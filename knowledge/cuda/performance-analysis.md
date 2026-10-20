# CUDA Performance Analysis

Concise entries on activity, throughput, Roofline, and dependency waits. Related: [[knowledge/cuda/execution-model|execution model]], [[knowledge/cuda/memory|memory]], and [[knowledge/cuda/instructions|instructions]]. Metric names, formulas, and support must be checked against the actual GPU and profiler version.

## I. Activity and Throughput Metrics

### 1. GPU Utilization

**Core idea: Common NVML GPU utilization measures time with kernel execution, not the fraction of peak arithmetic achieved.**

`nvidia-smi` reports a sampled busy-time percentage. A long-running kernel can keep it high while leaving most arithmetic capacity unused or waiting on memory. The NVML memory-utilization field is likewise activity time, not allocated-memory percentage or achieved bandwidth divided by peak. [Source: nvidia-smi utilization definitions](https://docs.nvidia.com/deploy/nvidia-smi/index.html).

### 2. SM Activity

**Core idea: DCGM SM activity accounts for where and when warps are active across the GPU.**

`DCGM_FI_PROF_SM_ACTIVE` averages the fraction of time with at least one active warp over SMs. Warps waiting on memory can count as active. A kernel occupying only a few SMs can therefore yield high NVML GPU utilization but low SM activity; neither metric is [[knowledge/cuda/execution-model#4. Occupancy|occupancy]]. [Source: DCGM profiling metrics](https://docs.nvidia.com/datacenter/dcgm/latest/user-guide/feature-overview.html#profiling-metrics).

### 3. Active Cycles

**Core idea: An active-cycle denominator excludes time when the measured hardware unit is inactive.**

For an SM, residency can keep cycles active even without instruction issue. Execution-pipeline activity is a different counter. Read the unit prefix and metric suffix: `.pct_of_peak_sustained_active` and `.pct_of_peak_sustained_elapsed` use different denominators and can produce different percentages for the same work. [Source: Nsight metric structure](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#metrics-structure).

### 4. Compute Throughput

**Core idea: Nsight's composite SM throughput highlights the most utilized constituent resource.**

Constituent counters are normalized against their own sustained peak rates; throughput metrics take the maximum constituent percentage. This is neither a sum of all pipe utilization nor an average fraction of all compute hardware. An FP64 kernel is not automatically compared with Tensor Core FLOP/s. Inspect the metric breakdown before identifying the bottleneck. [Source: Nsight throughput definitions](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#metrics-structure).

### 5. Issue Slots Busy

**Core idea: Measure instruction-issue activity rather than how long a downstream pipeline remains busy.**

It can be lower than an ALU activity percentage because issue and execution are different events, with different duration and aggregation. Multiple scheduler partitions, metric denominators, and architecture-specific issue width also matter. Two percentages alone cannot reveal how many instructions one scheduler can issue. [Sources: Nsight scheduler analysis](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#sections-and-rules); [[knowledge/cuda/execution-model#2. Instruction Issue|instruction issue]].

## II. Roofline Analysis

### 1. Roofline Model

**Core idea: Compare achieved arithmetic throughput with compute and data-movement ceilings.**

The basic bound is `P <= min(P_compute, bandwidth * arithmetic_intensity)`. Being far below a roof motivates further diagnosis, but proximity does not prove good algorithmic efficiency: redundant arithmetic can raise measured FLOP/s while making the useful task slower. Compare execution time and useful work as well as position on the chart. [Source: Nsight Roofline analysis](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#roofline-charts).

### 2. Arithmetic Intensity

**Core idea: Divide arithmetic work by bytes transferred at a specified memory level.**

HBM, L2, and L1 intensities can differ because reuse changes traffic between levels. State the byte boundary and FLOP convention, including whether an FMA counts as two operations. A tensor-size-only estimate can miss cache reuse and additional traffic. [Source: NVIDIA matrix-multiplication performance model](https://docs.nvidia.com/deeplearning/performance/dl-performance-matrix-multiplication/index.html).

### 3. Precision-Specific Roofs

**Core idea: Choose the ceiling that matches the executed arithmetic path.**

Two horizontal lines can represent FP32 and FP64 peaks, but a chart can also include Tensor Core or other ceilings. Read the legend and measured instruction mix; for an FP64 kernel, the relevant ceiling is not automatically the highest line. Device model and clock assumptions affect the values. [Source: Nsight Roofline charts](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#roofline-charts).

## III. Memory and Dependency Diagnosis

### 1. Local-Memory Reservation

**Core idea: Allocated local-memory capacity is different from executed local-memory traffic.**

CUPTI describes `localMemoryPerThread` and `localMemoryTotal_v2` as reserved bytes; the older 32-bit total field is deprecated. A zero per-thread display alongside a nonzero total does not establish a specific allocation cause or prove zero local accesses. Correlate the exact record/tool version with stack information and measured local load/store instructions or sectors. [Source: CUPTI kernel activity fields](https://docs.nvidia.com/cupti/api/structCUpti__ActivityKernel9.html).

### 2. Memory Latency

**Core idea: Measure the delay for the actual access path, rather than assign each storage name one universal cycle count.**

Hits, misses, contention, access width, bank conflicts, clocking, and dependency chains affect measurements. Bandwidth and latency are distinct; high throughput can coexist with long per-request latency. Published microbenchmarks provide architecture-specific reference points, not guaranteed shared/L1/L2/HBM timings for another GPU. [Source: Jia et al., memory-hierarchy measurements](https://arxiv.org/html/1903.07486v1).

### 3. Long Scoreboard

**Core idea: A warp is waiting on a dependency associated with the L1TEX operation path.**

Global, local, texture, and surface operations can produce this wait. It does not prove an HBM miss or saturated memory bandwidth. Find the producer instruction, then inspect access efficiency, caching, and available independent work. [Source: Nsight warp stall reasons](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#warp-stall-reasons).

### 4. Short Scoreboard

**Core idea: A warp is waiting on dependencies from other tracked operation paths, commonly MIO/shared-memory work.**

Shared loads are a common cause, but the category is not exclusive to them; operation coverage varies with hardware, including some constant-load paths. “Short” is a classification, not a guaranteed duration or a direct label for a SASS read barrier. [Source: Nsight hardware and stall definitions](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html).

### 5. Barrier Stall

**Core idea: A warp is waiting for peer warps to reach a block synchronization point.**

Uneven work before the barrier can cause the wait. This differs from [[knowledge/cuda/instructions#2. SASS Dependency Barriers|instruction dependency barriers]], which track result readiness or safe register reuse. Reducing sampled stalls helps only if the change removes work on the critical execution path; a stall percentage alone is not a speedup prediction. [Source: Nsight warp stall reasons](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#warp-stall-reasons).

## IV. Profiling Tools

### 1. Nsight Systems

**Core idea: Locate application-level gaps, transfers, launch costs, and overlap on a timeline.**

Use it to select the expensive phase or kernel before interpreting fine-grained hardware counters. Kernel properties such as reserved local memory are metadata, not a trace of each memory transaction. [Source: Nsight Systems user guide](https://docs.nvidia.com/nsight-systems/UserGuide/index.html).

### 2. Nsight Compute

**Core idea: Diagnose a selected kernel using counters, source/SASS correlation, and scheduler samples.**

Collect only the needed sections. Counter collection can replay kernels and alter cache state or normal concurrency; compare profiled evidence with normal execution time. Confirm formulas, GPU scope, and active/elapsed normalization before comparing metrics. [Source: Nsight profiling and replay](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html#replay).
