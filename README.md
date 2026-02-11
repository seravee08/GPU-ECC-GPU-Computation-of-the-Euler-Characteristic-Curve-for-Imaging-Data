# GPU-ECC-GPU-Computation-of-the-Euler-Characteristic-Curve-for-Imaging-Data
CUDA-accelerated computation of Euler Characteristic Curves. <br/>
Authors: Fan Wang, Hubert Wagner, Chao Chen <br/>
Paper: [GPU Computation of the Euler Characteristic Curve for Imaging Data](https://arxiv.org/pdf/2203.09087.pdf)

## Introduction
===============

GPU-ECC is cross-platform (Windows and Linux) and requires only **CUDA >= 12.6** to compile and run. We provide prebuilt binaries in two forms:

### Python extension
Install with 
```bash
pip install https://github.com/seravee08/GPU-ECC-GPU-Computation-of-the-Euler-Characteristic-Curve-for-Imaging-Data/raw/main/releases/gpuecc-0.1.0-cp312-cp312-linux_x86_64.whl
```
A complete usage example is provided in the Google Colab section.

### C++ binary (run from command line)
From the folder containing the executable, run:<br/>
```bash
GPU_ECC.exe [mode] [input] [output] [height] [width] [depth]
```


`GPU_ECC.exe [mode] [input_name] [output_name] [height] [width] [depth]` <br/>
Arguments:
<pre>
--mode:         GPU ECC can compute for a single file or for a batch of files. Use 's' for single mode or 'b' for batch mode.
        --b1:   spend all gpu resources on a single file one by one, good for large files
        --b2:   distribute gpu resources across several files, good for large number of small files
--input_name:   Path to a single file in single mode or a directory containing files in batch mode.
--output_name:  Path to a single flie in single mode or a directory in batch mode. In case of batch mode, the output file 
                will have the same name as input file.
--height:       Height of the input file. In case of batch mode, same height is assumed for every file under the directory.
--width:        Width of the input file. In case of batch mode, same width is assumed for every file under the directory.
--depth:        Depth of the input file. In case of 2D file, set depth to 0.
</pre>
An example command: <br/>
`GPU_ECC.exe b1 C:/input_directory C:/output_directory 256 256 0` <br/>



## Google Colab
===============

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
===============

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
- Create container and enter shell (Replace PATH_TO_DATA with an absolute path):
```command
docker run --name gpuecc -it --gpus=all -p 8888:8888 --mount type=bind,source="PATH_TO_DATA",target=/workspace -w /GPU-ECC --entrypoint /bin/bash seravee08/gpuecc:latest
```
