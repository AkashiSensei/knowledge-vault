# CUDA Knowledge

Short, independently addressable concepts drawn from the author's question wall and checked against primary documentation. Initial coverage includes 23 CUDA-related question chains, reviewed on 2026-10-19. Question-wall answers are learning context; architecture-specific observations are qualified rather than treated as universal specifications.

- [[knowledge/cuda/execution-model|Execution model]]: SM/SMSP hierarchy, warp residency, control flow, occupancy, TLP/ILP, and command submission.
- [[knowledge/cuda/memory|Memory and data movement]]: address spaces, caches, banks, sectors, wavefronts, and asynchronous copies.
- [[knowledge/cuda/instructions|Instructions and computation]]: PTX/SASS, registers, launch state, low precision, sparsity, and dependencies.
- [[knowledge/cuda/performance-analysis|Performance analysis]]: activity metrics, throughput, Roofline, memory observations, and stall diagnosis.

Related application-level notes: [[knowledge/ai-infra/inference|LLM inference]] and [[knowledge/ai-infra/parallelism|model parallelism]].

## I. Question-Wall Coverage

The IDs below identify the source chains in the personal homepage's `src/data/questions.json`; wording was read from its Chinese locale. They preserve provenance without duplicating the question-and-answer format in the concept notes.

| Source question ID | Concept entries |
| --- | --- |
| `gpu-sparsity` | [[knowledge/cuda/instructions#4. Structured Sparsity|Structured sparsity]] |
| `packed-low-precision` | [[knowledge/cuda/instructions#2. Packed Low-Precision Arithmetic|Packed arithmetic]]; [[knowledge/cuda/instructions#3. Tensor Cores|Tensor Cores]] |
| `roofline-kernel-quality` | [[knowledge/cuda/performance-analysis#1. Roofline Model|Roofline and useful work]] |
| `roofline-compute-peaks` | [[knowledge/cuda/performance-analysis#3. Precision-Specific Roofs|Precision-specific roofs]] |
| `sm-throughput` | [[knowledge/cuda/performance-analysis#4. Compute Throughput|Composite throughput]] |
| `local-memory-metrics` | [[knowledge/cuda/performance-analysis#1. Local-Memory Reservation|Local-memory reservation]] |
| `gpu-utilization` | [[knowledge/cuda/performance-analysis#1. GPU Utilization|GPU utilization]]; [[knowledge/cuda/performance-analysis#2. SM Activity|SM activity]] |
| `active-cycles` | [[knowledge/cuda/performance-analysis#3. Active Cycles|Active-cycle denominators]] |
| `alu-issue-slots` | [[knowledge/cuda/performance-analysis#5. Issue Slots Busy|Issue slots busy]] |
| `warp-scheduler` | [[knowledge/cuda/execution-model#1. Warp Scheduler|Warp scheduler]]; [[knowledge/cuda/execution-model#2. SM Subpartition (SMSP)|SMSP]]; [[knowledge/cuda/execution-model#2. Instruction Issue|instruction issue]] |
| `occupancy-steps` | [[knowledge/cuda/execution-model#4. Occupancy|Occupancy]]; [[knowledge/cuda/execution-model#5. Resource Allocation Granularity|allocation granularity]]; [[knowledge/cuda/execution-model#6. SMSP Occupancy|SMSP occupancy]] |
| `shared-wavefronts` | [[knowledge/cuda/memory#5. Excessive Wavefronts|Excessive wavefronts]] |
| `thread-index-registers` | [[knowledge/cuda/instructions#5. Special Registers|Special registers]] |
| `kernel-parameters` | [[knowledge/cuda/instructions#6. Kernel Parameters|Kernel parameters]] |
| `local-stack-base` | [[knowledge/cuda/instructions#7. Local Stack Frame|Local stack frame]] |
| `simt-branches` | [[knowledge/cuda/execution-model#1. SIMT Divergence|Divergence]]; [[knowledge/cuda/execution-model#2. Predication|predication]]; [[knowledge/cuda/execution-model#3. Independent Thread Scheduling|independent scheduling]] |
| `sass-integer-instructions` | [[knowledge/cuda/instructions#1. Integer Instructions|Integer instructions]] |
| `gpu-memory-hierarchy` | [[knowledge/cuda/memory#I. Storage and Address Spaces|Storage and address spaces]]; [[knowledge/cuda/performance-analysis#2. Memory Latency|memory latency]] |
| `gpu-register-allocation` | [[knowledge/cuda/instructions#3. Register Allocation|Register allocation]]; [[knowledge/cuda/instructions#4. Register Spilling|spilling]] |
| `l1-shared-memory-wavefronts` | [[knowledge/cuda/memory#2. Sector|Sector]]; [[knowledge/cuda/memory#3. Bank Conflict|bank conflict]]; [[knowledge/cuda/memory#4. Wavefront|wavefront]] |
| `scoreboard-read-write-barriers` | [[knowledge/cuda/instructions#1. Scoreboard|Scoreboard]]; [[knowledge/cuda/instructions#2. SASS Dependency Barriers|dependency barriers]]; [[knowledge/cuda/instructions#3. Dependency Counters|dependency counters]]; [[knowledge/cuda/performance-analysis#III. Memory and Dependency Diagnosis|stall diagnosis]] |
| `async-copy-l2-cache` | [[knowledge/cuda/memory#1. cp.async|cp.async]]; [[knowledge/cuda/memory#2. Tensor Memory Accelerator|TMA]]; [[knowledge/cuda/memory#6. L2 Cache|L2]] |
| `pushbuffer-gpfifo-memory-location` | [[knowledge/cuda/execution-model#1. Push Buffer|Push buffer]]; [[knowledge/cuda/execution-model#2. GPFIFO|GPFIFO]] |

## II. Illustration Provenance

- `assets/nvidia-gpu-microarchitecture.svg` is an unchanged copy of the user-supplied `nvidia_gpu_microarchitecture_clean_layout.svg` from the local CUDA learning collection. Its Chinese labels and Hopper scope are preserved; no external authorship is inferred. It appears in [[knowledge/cuda/execution-model#I. Hardware Organization|hardware organization]] and [[knowledge/cuda/memory#I. Storage and Address Spaces|memory storage]].
- Mermaid diagrams are original explanatory schematics. Their arrows describe control flow, compilation/resource assignment, or command references, as stated beside each diagram.
