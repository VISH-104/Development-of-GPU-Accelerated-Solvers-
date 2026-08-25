# 🚀 GPU-Accelerated Finite Difference Method Solver

### High-Performance 2D Compressible-Flow Solver using CuPy & CUDA C

---

## 🎯 Project Overview

Developed a **GPU-accelerated 2D compressible-flow solver** using the **Finite Difference Method (FDM)** with **CuPy and CUDA C** for efficient simulation of shock-dominated compressible flows on NVIDIA GPUs.

The project combines **compressible-flow numerical methods, GPU kernel programming, memory optimization, performance profiling, and HPC benchmarking** to develop a high-performance CFD solver capable of handling large computational domains.

---

## 🎯 Objectives

* Develop a **GPU-accelerated 2D compressible-flow FDM solver** for accurate resolution of **shocks, contact discontinuities, and expansion waves**.
* Implement and optimize **spatial reconstruction, flux evaluation, and time integration** while minimizing **memory traffic, synchronization, and kernel-launch overhead**.
* Benchmark **large-scale CFD performance and scalability**, including **MPI communication and distributed-memory execution**.


## 🔬 Numerical Methodology

The solver advances the **2D compressible Euler equations** using a finite-difference formulation with shock-capturing schemes.

| Component | Method |
|---|---|
| Governing Equations | **2D Compressible Euler** |
| Spatial Scheme | **Finite Difference Method (FDM)** |
| Reconstruction | **2nd-Order MUSCL + Minmod TVD** |
| Flux Solvers | **Rusanov / HLLC** |
| Time Integration | **Euler / 3rd-Order RK3** |
| Time Stepping | **Adaptive CFL** |
| GPU Framework | **CuPy + CUDA C** |
| Memory Layout | **Structure of Arrays (SoA)** |

### Key Features

- **MUSCL + Minmod:** Second-order shock-capturing reconstruction with TVD limiting.
- **Rusanov / HLLC:** Robust flux evaluation with improved shock and contact-discontinuity resolution.
- **Euler / RK3:** Explicit time integration with adaptive CFL-based time stepping.
---

## 🔄 Computational Workflow

2D Compressible Euler → FDM → MUSCL + Minmod TVD → Rusanov / HLLC
→ Euler / RK3 → Adaptive CFL → GPU Execution
---

## ⚡ GPU Implementation & Optimization

The solver was progressively optimized through a **five-stage GPU pipeline** targeting **kernel efficiency, memory traffic, and data reuse**.

### Optimization Pipeline

Naive CuPy → Fused Rusanov → Fused HLLC → Tiled Rusanov → Tiled HLLC → Optimized GPU Solver


### 🔑 Key Optimizations

- **Kernel Fusion:** Reduced kernel launches and intermediate global-memory operations.
- **Shared-Memory Tiling:** Improved stencil-data reuse and reduced global-memory traffic.
- **Coalesced Access:** Improved memory-access efficiency and effective bandwidth.
- **Float4 Vectorization:** Enhanced state-variable loading and memory throughput.
- **SoA Layout:** Optimized flow-variable organization for GPU execution.
- **Warp-Level CFL Reduction:** Reduced memory traffic and synchronization through on-GPU CFL computation.


## 🧪 Validation, Profiling & Performance

### ✅ Numerical Validation

Validated the solver using the **2D Sod Shock-Tube / Riemann problem** to verify accurate resolution of:

- **Shock waves**
- **Contact discontinuities**
- **Expansion waves**
- **Pressure and density variations**

### 🔎 GPU Performance Profiling

Profiled the optimized solver using **NVIDIA Nsight Compute** to analyze **SM/GPU utilization, FP32 throughput, occupancy, memory bandwidth, and kernel efficiency**. The analysis identified the solver as predominantly **memory-bound**, highlighting the importance of memory traffic and data reuse.

### 📊 Large-Scale Benchmarking

Benchmarked progressively larger grids up to **16384 × 2048 (33.5M cells)**, demonstrating **near-O(N) scaling** while maintaining shock-resolution capability.

**Grid Scaling:** `1024 × 128 → 2048 × 256 → 4096 × 512 → 8192 × 1024 → 16384 × 2048`

### 🏆 Performance Highlights

| Metric | Result |
|---|---:|
| **Maximum Grid** | 16384 × 2048 |
| **Problem Size** | 33.5M cells |
| **FP32 Utilization** | ~22–23% peak |
| **Peak Throughput** | ~5000 MCUPS |
| **GPU Occupancy** | Up to ~87% |
| **Scaling** | Near O(N) |
| **Profiler** | NVIDIA Nsight Compute |

### 🔄 Performance Workflow

**Validation → Nsight Profiling → Bottleneck Identification → Kernel/Memory Optimization → Large-Scale Benchmarking → Scaling Analysis**
---

## 🌐 MPI & HPC Benchmarking

Benchmarked **MPI communication** to quantify **communication overhead, data-exchange cost, and distributed-memory scalability**, providing a foundation for future **multi-GPU/HPC extensions**.

### 🛠️ Tools & Technologies

- **CFD:** FDM, Compressible Euler, MUSCL, Minmod TVD, Rusanov/HLLC, Euler/RK3, Adaptive CFL
- **GPU:** Python, CuPy, CUDA C, Kernel Fusion, Shared Memory, Float4, Coalesced Access, SoA
- **HPC:** NVIDIA Nsight Compute, GPU Profiling, Memory Analysis, MPI

### 💡 Key Contributions

- Developed a **GPU-accelerated 2D compressible-flow FDM solver** using **CuPy + CUDA C**.
- Implemented **MUSCL–Minmod, Rusanov/HLLC, Euler/RK3, and adaptive CFL** schemes for shock-dominated flows.
- Designed a **five-stage GPU optimization pipeline** using kernel fusion, shared-memory tiling, vectorization, and optimized memory access.
- Validated the solver using the **2D Sod shock-tube** and scaled simulations to **33.5M cells (16384 × 2048)**.
- Achieved **~22–23% peak FP32 utilization, ~5000 MCUPS, up to ~87% occupancy, and near-O(N) scaling**.
- Used **Nsight Compute** for profiling-driven optimization and benchmarked **MPI communication/scalability**.

### 🔄 Project Workflow

**Numerical Solver → GPU Implementation → Kernel/Memory Optimization → Validation → Nsight Profiling → Large-Scale Benchmarking → MPI/HPC Analysis**

### 📌 Project Takeaway

**CFD Numerical Methods + CUDA/GPU Computing + Memory Optimization + Performance Engineering + HPC/MPI** for scalable, shock-dominated CFD simulations.
