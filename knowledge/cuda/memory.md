# CUDA Memory and Data Movement

Concise entries on storage, access patterns, and asynchronous copies. Address spaces and physical cache paths are different layers of description.

## I. Storage and Address Spaces

![Hopper H100 conceptual organization showing registers, L1/shared memory, L2, HBM, and asynchronous copy paths](assets/nvidia-gpu-microarchitecture.png)

*Reproduced unchanged from the user's local learning diagram, `nvidia_gpu_microarchitecture_clean_layout.png`, with its original Chinese labels preserved. Focus on the storage locations and data-movement paths. This is a Hopper H100 / SM90 conceptual map; shared L1/shared-memory SRAM does not make their access semantics identical, and register bypass does not mean cache bypass. Technical reference: [Hopper tuning guide](https://docs.nvidia.com/cuda/hopper-tuning-guide/index.html).*

### 1. Registers

**Core idea: Keep a thread's working values in the SM register file.**

The compiler allocates registers to live values, and resident threads retain separate state. Registers do not pass through L1/L2 for ordinary operand accesses, but instruction dependencies and register-file constraints still affect execution. See [[knowledge/cuda/instructions#3. Register Allocation|register allocation]]. [Source: PTX register state](https://docs.nvidia.com/cuda/parallel-thread-execution/index.html#register-state-space).

### 2. Global Memory

**Core idea: Provide device-accessible storage shared across threads and kernel launches.**

Ordinary device allocations are backed by device memory, commonly HBM or GDDR. Loads and stores use the memory hierarchy according to instruction and cache policy; a global access does not imply a DRAM transaction. Managed and mapped system memory broaden where accessible data can physically reside. [Source: CUDA memory model](https://docs.nvidia.com/cuda/cuda-programming-guide/01-introduction/programming-model.html).

### 3. Local Memory

**Core idea: Give each thread private memory-backed storage when values are not kept in registers.**

Private arrays, stack frames, and traditional register spills can use local memory. It is an address space distinct from global memory, although both are ordinarily backed by device memory and caches. “Local” describes thread scope, not on-chip placement; identical local addresses in different threads remain private. [Source: PTX local state](https://docs.nvidia.com/cuda/parallel-thread-execution/index.html#local-state-space).

### 4. Shared Memory

**Core idea: Explicitly manage on-chip storage for cooperating threads.**

Ordinary shared allocations belong to a block. Threads access them directly through shared-memory operations, without first checking L1 then L2. Some GPUs partition one SRAM resource between L1 and shared memory; that does not merge their semantics. Hopper clusters additionally support distributed shared-memory access across cooperating blocks. [Sources: SIMT kernel storage](https://docs.nvidia.com/cuda/cuda-programming-guide/02-basics/writing-cuda-kernels.html); [Hopper tuning](https://docs.nvidia.com/cuda/hopper-tuning-guide/index.html).

### 5. L1TEX

**Core idea: An SM-side subsystem services caching and memory-request processing.**

Nsight models tag, miss, and data stages within L1TEX. Global, local, texture, and surface operations can use its paths, while cache policies may bypass L1 data caching. A request passing through the subsystem need not hit its cache or require the same number of processing cycles as another request. [Source: Nsight hardware model](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#metrics-hw-model).

### 6. L2 Cache

**Core idea: Share cached device-memory data across SMs before accessing external memory.**

L2 hits can avoid external-memory reads; stores and writeback behavior also involve the cache hierarchy. Requests may originate from SM loads, asynchronous copies, or other GPU engines. Thus, measured device-wide L2 traffic is not always attributable solely to one profiled kernel. [Source: Nsight hardware model](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#metrics-hw-model).

### 7. Constant Memory

**Core idea: Supply read-only data through constant-access mechanisms optimized for uniform reads.**

A warp reading one address can benefit from broadcast; multiple distinct addresses can require additional servicing. Kernel arguments and `__constant__` objects are related uses, not identical ABI objects. Constant-cache organization and instructions vary by GPU, so a single universal L1TEX-only path is misleading. [Source: NVIDIA constant-cache model](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#metrics-hw-model).

### 8. Texture Memory

**Core idea: Access CUDA arrays or linear resources through texture sampling semantics.**

Texture objects support features such as addressing modes and filtering for supported formats. Texture caching favors spatial locality; “texture memory” does not mean a separate external-memory technology. Hardware paths and performance depend on the access and architecture. [Source: PTX texture instructions](https://docs.nvidia.com/cuda/parallel-thread-execution/index.html#texture-instructions).

### 9. Surface Memory

**Core idea: Read or write CUDA-array resources through surface operations.**

Surfaces provide typed array access without texture filtering. They use device-memory-backed resources and relevant cache paths; they are not a separate rung between global memory and DRAM. [Source: PTX surface instructions](https://docs.nvidia.com/cuda/parallel-thread-execution/index.html#surface-instructions).

## II. Access Patterns and Memory Work

### 1. Memory Coalescing

**Core idea: Combine a warp's addresses into efficiently serviced memory transactions.**

Nearby, suitably aligned addresses often require fewer sectors than scattered addresses for the same useful bytes. Coalescing is determined by the collective addresses and access width, not just whether each individual thread accesses contiguous data over time. [Source: CUDA global-memory access examples](https://docs.nvidia.com/cuda/cuda-programming-guide/02-basics/writing-cuda-kernels.html).

### 2. Sector

**Core idea: A sector is a cache-transfer/accounting unit, not a warp or instruction.**

In Nsight's documented L1/L2 model, a sector is 32 bytes and a cache line is 128 bytes. One instruction can request multiple sectors, and the same sector count can lead to different internal [[knowledge/cuda/memory#4. Wavefront|wavefront]] counts. Interpret sector efficiency at the specified cache level. [Source: Nsight memory model](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#metrics-hw-model).

### 3. Bank Conflict

**Core idea: Different shared-memory words competing for one bank can require serialized servicing.**

For the common 32-bank, 32-bit-word model, consecutive words map across banks. Several lanes reading the same word can broadcast rather than conflict; different words in the same bank are the problematic case. Wider accesses may require several conflict-free service rounds, so multiple wavefronts alone do not prove a conflict. [Source: CUDA shared-memory access examples](https://docs.nvidia.com/cuda/cuda-programming-guide/02-basics/writing-cuda-kernels.html).

### 4. Wavefront

**Core idea: A wavefront is one internally parallel work package at a memory-pipeline stage.**

One warp memory request can create multiple wavefronts. Shared-memory servicing depends on width and banks; global/local L1TEX servicing depends on tags, sectors, and stage limits. A wavefront is neither a cache line nor another name for a CUDA warp. Sector count alone does not determine it. [Source: Nsight request/sector/wavefront model](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#metrics-hw-model).

For a shared-memory load, bank conflicts require successive service rounds. Returned data passes through the crossbar and a per-SMSP FIFO to the register file. Only after all participating lanes' results reach the register file does the load complete and release its result dependency. An intermediate wavefront does not release it; inactive or predicated-off lanes are excluded. In the [[knowledge/cuda/instructions#3. Dependency Counters|dependency-counter model]], completion decrements the load's assigned counter; a consumer waiting for zero can proceed only when all operations grouped there have completed. [Source: NVIDIA engineer's shared-load walkthrough](https://forums.developer.nvidia.com/t/requesting-clarification-for-shared-memory-bank-conflicts-and-shared-memory-access/268574/12).

### 5. Excessive Wavefronts

**Core idea: Compare actual wavefront work against the profiler's instruction-specific ideal.**

The source metric `derived__memory_l1_wavefronts_shared_excessive` reports achieved minus ideal work. Its baseline depends on operation width and participating, non-predicated-off threads. Bank conflicts can add servicing work, but this is not simply “wavefronts minus one”; inspect actual/ideal counts and bank-conflict metrics together. [Source: Nsight source metrics](https://docs.nvidia.com/nsight-compute/NsightCompute/index.html#source-page).

## III. Asynchronous Data Movement

The overview image compares the paths. These mechanisms bypass register staging, not the entire memory hierarchy.

### 1. cp.async

**Core idea: Copy global data into shared memory without a general-purpose register staging step.**

The classic Ampere `cp.async` / LDGSTS path supports global-to-shared copies on SM80+, not shared-to-global copies. It can overlap copying with other work when the schedule permits. Cache operators control L1 behavior, while the global-memory side still uses L2; an L2 hit need not access HBM. [Sources: Ampere tuning](https://docs.nvidia.com/cuda/ampere-tuning-guide/index.html); [PTX cp.async](https://docs.nvidia.com/cuda/parallel-thread-execution/index.html#data-movement-and-conversion-instructions-cp-async).

### 2. Tensor Memory Accelerator

**Core idea: Offload bulk and tensor-tile transfers, including address generation, to Hopper's TMA facilities.**

SM90+ TMA supports global-to-shared and shared-to-global movement; multidimensional tensor transfers use a tensor map. Bypassing register staging reduces instruction and register pressure but does not bypass L2 or guarantee a speedup. Alignment, layout, transfer size, and synchronization requirements matter. [Sources: Hopper tuning](https://docs.nvidia.com/cuda/hopper-tuning-guide/index.html); [CUDA asynchronous copies](https://docs.nvidia.com/cuda/cuda-programming-guide/04-special-topics/async-copies.html).

### 3. Asynchronous Copy Completion

**Core idea: Issuing a copy does not make its data immediately safe to consume or overwrite.**

Use the operation's completion protocol, such as async-group waits or transaction barriers, plus required thread coordination and proxy ordering. TMA load and store directions use different completion mechanisms; a wait may guarantee source-buffer reuse without implying global visibility of every destination write. A generic block barrier alone is not a replacement for all copy-completion requirements. [Source: CUDA asynchronous-copy completion tables](https://docs.nvidia.com/cuda/cuda-programming-guide/04-special-topics/async-copies.html).
