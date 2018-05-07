### ROCM:OPEN SOURCE PLATFORM FOR HPC AND ULTRASCALE GPU COMPUTING

#### 简介

- HPC/Hyperscale-class platform for GPU computing，服务器节点间用RDMA交互，无缝的集成CPU计算和GPU计算


- 利用Heterogeneous System Architecture (HSA) Runtime API ，语言独立

#### 重要特性

- Multi-GPU coarse-grain shared virtual memory 存储管理和性能
- Process concurrency and preemption 计算资源调度
- Large memory allocations 存储申请的性能
- HSA signals and atomics 异构计算的同步
- User-mode queues and DMA 快速的数据交互，避免一次内核态拷贝
- Standardized loader and code-object format 规范？具体不清楚
- Dynamics and offline-compilation support 实时和离线编译
- Peer-to-peer multi-GPU operation with RDMA support 快速交互
- Profiler trace and event-collection API 性能分析
- Systems-management API and tools 系统管理

#### 具体模块

- GCN(Graphics Core Next)汇编：AMD架构相关汇编器
- LLVM(Low Level Virtual Machine)编译
- HCC(Heterogeneous Computing Compiler?), HIP?
- 语言的运行时环境，driver等等


