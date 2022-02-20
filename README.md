---
typora-root-url: .
---

# Advanced_Physics_Engines

![2022-02-20_16-21](pic/2022-02-20_16-21.png)

[class link](https://www.bilibili.com/video/BV1ZK411H7Hc?spm_id_from=333.999.0.0)

[official website](https://yuanming.taichi.graphics/teaching/2020-games201/)

[documentation](https://docs.taichi.graphics/)

## The Taichi Programming Language

### What is Taichi?

High-performance domain-specific language embedded in Python

- Designed for computer graphics applications with productivity and
  portability in mind
- Data-oriented, parallel, megakernels
- Decouple data structures from computation
- Access spatially sparse tensors as if they are dense
- Differentiable programming support

### Getting started

#### Installation

Taichi can be installed via pip on 64-bit Python 3.6/3.7/3.8:

```bash
python3 -m pip install taichi
```

- Taichi supports Windows, Linux, and OS X.
- Taichi runs on both CPUs and GPUs (CUDA/OpenGL/Apple Metal).
- Build from scratch if your CPU is AArch64 or you use Python 3.9+

#### Initialization

Always initialize Taichi with `ti.init()` before you do any Taichi operations.
For example,

```python
ti.init(arch=ti.cuda)
```

The most useful argument: arch , i.e., the backend (architecture) to use

- `ti.x64/arm/cuda/opengl/metal` : stick to a certain backend.
- `ti.cpu (default)`, automatically detects x64/arm CPUs.
- `ti.gpu` , try cuda/metal/opengl . If none is detected, Taichi falls back on CPUs.

### Data

#### Data types

Taichi is strongly typed. Supported basics types include

- Signed integers: `ti.i8/i16/i32/i64`
- Unsigned integers: `ti.u8/u16/u32/u64`
- Float-point numbers: `ti.f32/f64`

`ti.i32` and `ti.f32` are the most commonly used types in Taichi. Boolean values
are represented by `ti.i32` for now.

The CPU and CUDA backends support all data types. Other backend may miss
certain data type support due to backend API constraints. See the [documentation](https://docs.readthedocs.io/en/stable/)
for more details.

#### Tensors

Taichi is a data-oriented programming language where tensors are first-class
citizens.

- Tensors are essentially multi-dimensional arrays
- An element of a tensor can be either a scalar ( `var` ), a vector ( `ti.Vector` ), or a matrix ( `ti.Matrix` )
- Tensor elements are always accessed via the `a[i, j, k]` syntax. (No pointers!)
- Access out-of-bound is undefined behavior
- (Advanced) Tensors can be spatially sparse

##### Tensors v.s. Matrices in Taichi

Although mathematically matrices are treated as 2D tensors, in Taichi, tensor and
matrix are two completely different concepts. Matrices can be used as tensor
elements, so you can have tensors with each element being a matrix.

#### Example

![2022-02-20_15-34](pic/2022-02-20_15-34.png)

### Computation

#### Kernels

![2022-02-20_15-37](pic/2022-02-20_15-37.png)

#### Functions

![2022-02-20_16-06](pic/2022-02-20_16-06.png)

#### Scalar math

![2022-02-20_16-10](pic/2022-02-20_16-10.png)

#### Matrices and linear algebra

![2022-02-20_16-11](/pic/2022-02-20_16-11.png)

#### Parallel for-loops

![2022-02-20_16-11_1](/pic/2022-02-20_16-11_1.png)

##### Range-for loops

![2022-02-20_16-13](pic/2022-02-20_16-13.png)

![2022-02-20_16-13_1](pic/2022-02-20_16-13_1.png)

##### Struct-for loops

![2022-02-20_16-14](pic/2022-02-20_16-14.png)

#### Atomic Operations

![2022-02-20_16-15](pic/2022-02-20_16-15.png)

#### Taichi-scope v.s. Python-scope

![2022-02-20_16-30](pic/2022-02-20_16-30.png)

![2022-02-20_16-29](pic/2022-02-20_16-29.png)

#### Phases of a Taichi program

![2022-02-20_16-31](/pic/2022-02-20_16-31.png)

#### Putting everything together

![2022-02-20_17-11](pic/2022-02-20_17-11.png)

### Debugging

![2022-02-20_17-53](pic/2022-02-20_17-53.png)

### Exporting your results

![](pic/2022-02-20_21-02.png)

## Lagrangian v.s. Eulerian: Two Views of Continuums

![2022-02-20_20-25](pic/2022-02-20_20-25.png)

![2022-02-20_20-25_1](pic/2022-02-20_20-25_1.png)

![](pic/2022-02-20_20-26.png)

![](pic/2022-02-20_20-28.png)

### Lagrangian Simulation Approaches

Topics:

- 弹簧质点系统（Mass-spring systems）：你的第一个物理模拟器
- 显式与隐式时间积分器（Explicit/implicit time integrators）
- 光滑粒子流体动力学（Smoothed particle hydrodynamics）
- 快速邻居搜索（Neighborhood search）
- 基于四面体网格（tetrahedral mesh）的拉格朗日有限元模拟
- 隐式有限元求解器（Implicit FEM solvers）
- 边界条件处理
- Taichi编程语言高级特性

#### Mass-Spring Systems

![](pic/2022-02-20_20-38.png)

#### Time integration

![](pic/2022-02-20_20-39.png)

##### Implementing a mass-spring system with symplectic Euler

![](pic/2022-02-20_20-41.png)

![](pic/2022-02-20_20-41_1.png)

##### Explicit v.s. implicit time integrators

![](pic/2022-02-20_20-44.png)

##### Mass-spring systems' time integration

![](pic/2022-02-20_20-45.png)

![](pic/2022-02-20_20-46.png)

![](pic/2022-02-20_20-48.png)

![](pic/2022-02-20_20-48_1.png)

![](pic/2022-02-20_20-48_2.png)

##### Unifying explicit and implicit integrators

![](pic/2022-02-20_20-50.png)

##### Solve faster

![](pic/2022-02-20_20-51.png)

#### Smoothed Particle Hydrodynamics (SPH)

[SPH Tutorial](https://interactivecomputergraphics.github.io/SPH-Tutorial/)

![](pic/2022-02-20_20-53.png)

![](pic/2022-02-20_20-54.png)

##### Implementing SPH using the Equation of States (EOS)

![](pic/2022-02-20_20-54_1.png)

##### Gradients in SPH

![](pic/2022-02-20_20-55.png)

##### SPH Simulation Cycle

![](/pic/2022-02-20_20-56.png)

##### Variants of SPH

![](pic/2022-02-20_20-57.png)

##### Courant–Friedrichs–Lewy (CFL) condition

![](pic/2022-02-20_20-57_1.png)

##### Accelerating SPH: Neighborhood search

![](pic/2022-02-20_20-58.png)

##### Other particle-based simulation methods

![](pic/2022-02-20_20-59.png)

