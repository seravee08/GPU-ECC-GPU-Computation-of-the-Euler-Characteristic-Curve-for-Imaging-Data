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

