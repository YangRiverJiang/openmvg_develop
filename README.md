# openMVG Experimental Fork

[![Original Repository](https://img.shields.io/badge/upstream-openMVG-brightgreen)](https://github.com/openMVG/openMVG)
[![Status](https://img.shields.io/badge/status-experimental-red)]()
[![License](https://img.shields.io/badge/license-MPL--2.0-blue)](LICENSE)

**⚠️ Experimental Fork Notice**  
This is a custom research fork of [openMVG](https://github.com/openMVG/openMVG) focused on experimental features based on Windows.
**Currently, it is not stable to build.**
It is not affiliated with the official openMVG project.

## 🔬 Research Focus Areas

### GPU Acceleration
- CUDA-accelerated feature extraction
- GPU-based bundle adjustment

### Modern Dependency Support
- **Experimental Ceres Solver 2.2.0 integration**
- Updated Eigen/Ceres solver compatibility
- C++17/20 features adoption

### Large-Scale Processing
- Enhanced storage and memory management

## 🛠️ Build Environment

| Component       | Version               | Notes                      |
|-----------------|-----------------------|----------------------------|
| CMake           | 3.25      | Minimum supported version is 3.24, cmake versions after 3.30 are not recommended for now  |
| MSVC Toolset    | v143 (VS2022)         | 19.30+ compiler required   |
| [Ceres Solver](https://github.com/ceres-solver/ceres-solver)    | 2.2.0  | To be compiled with CUDA and cuDSS       |
| [CUDA](https://developer.nvidia.com/cuda-toolkit)           | 12.9                | GPU features require CUDA  |
| [cuDSS](https://developer.nvidia.com/cudss)           | 0.6                | High-performance CUDA Library for Direct Sparse Solvers |

[Quick link](https://cmake.org/files/v3.25/cmake-3.25.3-windows-x86_64.zip) to download CMake 3.25.

### Build Instructions


- Open cmake-gui, configure, and generate Ceres with GPU support. The basic details can be found [here](http://ceres-solver.org/installation.html#windows). Additionally, ensure CUDA-related entries are set.
  1. ```CMAKE_CUDA_ARCHITECTURES``` is set to ```native```.
  2. ```CUDAToolkit_BIN_DIR``` is set to ```C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.9\bin```.
  3. ```USE_CUDA``` is set to ```default```.
  4. ```cudss_DIR``` is set to ```C:\Program Files\NVIDIA cuDSS\v0.6\lib\12\cmake\cudss```.
- Build Ceres using:
  ```cmd
  cmake --build . --config Release --target ALL_BUILD
  ```
- Download the openMVG from this fork.
  ```cmd
  git clone --recursive https://github.com/YangRiverJiang/openmvg_develop.git
  ```
- Open another cmake-gui, configure, and generate this openMVG with the Ceres you built.
  1. ```Ceres_DIR``` and ```CERES_DIR_HINTS``` are set to the ```lib\cmake\Ceres``` subfolder of the Ceres.
  2. ```absl_DIR``` is set to the ```lib\cmake\absl``` subfolder of the Ceres.
  3. ```cudss_DIR``` is set to ```C:\Program Files\NVIDIA cuDSS\v0.6\lib\12\cmake\cudss```.
  4. Upon ```configure```, you should see external Ceres and CUDA information from the output. Click ```Open Project``` and compile the entire openMVG solution.
  5. In the Visual Studio project openMVG_sfm, add preprocessor ```SFM_USE_GPU``` to test GPU-enabled Ceres for openMVG sfm.
  




