# GPU-ECC-GPU-Computation-of-the-Euler-Characteristic-Curve-for-Imaging-Data
CUDA-accelerated computation of Euler Characteristic Curves. <br/>
Authors: Fan Wang, Hubert Wagner, Chao Chen <br/>
Paper: [GPU Computation of the Euler Characteristic Curve for Imaging Data](https://arxiv.org/pdf/2203.09087.pdf)

## Google Colab

We provide a **GPU-ECC-demo** notebook on Google Colab that demonstrates how to use GPU-ECC.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/seravee08/GPU-ECC-GPU-Computation-of-the-Euler-Characteristic-Curve-for-Imaging-Data/blob/main/GPU_ECC_demo.ipynb)

The notebook provides a step-by-step workflow:

1. **Environment setup**
   - Installs the precompiled `gpu-ecc` wheel for Python 3.12 on Linux.

2. **Data loading**
   - Downloads a sample 2D Gaussian random field (`.dat`) from this repository.
   - Downloads a sample 3D Gaussian random field (`.dat`) from this repository.

3. **Running GPU-ECC**
   - Creates a 2D GPU-ECC instance and computes ECC from an input file path.
   - Creates a 3D GPU-ECC instance and computes ECC from an input NumPy array.
   - (Optional) Saves the results to a file.

## Docker Image

Inside the Dokcer image, we provide:
- Source code under ```:/GPU-ECC/source```
- Compiled C++ binary: ```GPUECC```
- Compiled Python extension: ```gpuecc.cpython-312-x86_64-linux-gnu.so```
- A sample notebook demonstrating how to use GPU-ECC
- Sample data

### Prerequisites
**Windows 10/11**
- Docker Desktop with WSL 2 backend enabled.
- NVIDIA GPU + up-to-date Windows NVIDIA driver.

**Linux**
- NVIDIA GPU + driver installed on the host.
- NVIDIA Container Toolkit installed and configured for Docker.

### Run Docker
- Pull image: ```docker pull seravee08/gpuecc:latest```
- Create container and enter shell (Replace PATH_TO_DATA with an absolute Windows path):
```command
docker run --name gpuecc -it --gpus=all -p 8888:8888 --mount type=bind,source="E:\WorkBench\GPU-ECC",target=/workspace -w /GPU-ECC --entrypoint /bin/bash seravee08/gpuecc:latest
```

