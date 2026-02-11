# GPU-ECC-GPU-Computation-of-the-Euler-Characteristic-Curve-for-Imaging-Data
CUDA-accelerated computation of Euler Characteristic Curves.
Authors: Fan Wang, Hubert Wagner, Chao Chen <br/>
Paper: [GPU Computation of the Euler Characteristic Curve for Imaging Data](https://arxiv.org/pdf/2203.09087.pdf)

## Google Colab

A **TopoGPU-demo** notebook is provided to make it easy to try TopoGPU without installing it locally.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/seravee08/GPU-ECC-GPU-Computation-of-the-Euler-Characteristic-Curve-for-Imaging-Data/blob/main/GPU_ECC_demo.ipynb)

The notebook provides a step-by-step workflow:

1. **Environment setup**
   - Installs the precompiled `topogpu` wheel for Python 3.12 on Linux.
   - Installs `cripser` (which provides the `tcripser` interface).

2. **Data loading**
   - Downloads a sample 3D grayscale volume (`.raw`) from this repository.

3. **Running TopoGPU**
   - Demonstrates `topogpu.create3D(...)` and explains its key parameters.
   - Runs persistent homology on the sample volume and retrieves the resulting pairs.

4. **Running Cubical Ripser (tcripser)**
   - Computes persistence with `tcripser.computePH(...)` on the same volume.
   - Extracts the persistence pairs from the `tcripser` output.

5. **Result comparison**
   - Compares TopoGPU and Cubical Ripser outputs (up to 3 decimal places).
   - Reports any nontrivial persistence pairs that differ between the two methods.
