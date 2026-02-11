# GPU-ECC-GPU-Computation-of-the-Euler-Characteristic-Curve-for-Imaging-Data
CUDA-accelerated computation of Euler Characteristic Curves. <br/>
Authors: Fan Wang, Hubert Wagner, Chao Chen <br/>
Conference paper: [GPU Computation of the Euler Characteristic Curve for Imaging Data](https://arxiv.org/pdf/2203.09087.pdf)<br/>
Journal paper with significant improvements: [GPU Computation of the Eule Characteristic Curve for Imaging Data](https://jocg.org/index.php/jocg/article/view/4470/3397)<br/>
If you use GPU-ECC in your work, please cite both papers.

## Introduction

GPU-ECC is cross-platform (Windows and Linux) and requires only **CUDA >= 12.6** to compile and run. We provide prebuilt binaries in two forms:

### Python extension
Install with 
```bash
pip install https://github.com/seravee08/GPU-ECC-GPU-Computation-of-the-Euler-Characteristic-Curve-for-Imaging-Data/raw/main/releases/gpuecc-0.1.0-cp312-cp312-linux_x86_64.whl
```
Import GPU-ECC
```bash
import gpuecc
```
A complete usage example is provided in the **Google Colab** section.

### C++ binary (run from command line)
From the folder containing the executable, run:<br/>
```bash
GPU_ECC.exe [mode] [input] [output] [height] [width] [depth]
```
Arguments:
<pre>
--mode:         GPU ECC can compute for a single file or for a batch of files. Use 's' for single mode or 'b' for batch mode.
--input:        directory for batch mode, file for single mode
--output:       directory for batch mode, file for single mode
--height:       height of the input file. In case of batch mode, same height is assumed for every file under the directory.
--width:        width of the input file. In case of batch mode, same width is assumed for every file under the directory.
--depth:        depth of the input file. In case of 2D file, set depth to 0.
</pre>
An example command:
```command
./GPU_ECC b C:/input_directory C:/output_directory 256 256 0`
```
The C++ binary is included in the Docker image—see the **Docker Image** section for details.

### Inputs/Outputs
GPU-ECC accepts files with floating numbers in binary form. The filename extension should be .dat. We use the following code snippet to write data that is used as test inputs for GPU ECC:
```
std::ofstream wstream(filename.c_str(), std::ios::out | std::ios::binary);
for (size_t i = 0; i < size; i++) { float o = (float)data[i]; wstream.write((char*)&o, sizeof(float)); }
wstream.close();
```
Some examples are provided under folder "data". ECC GPU writes the ECC results into .txt files.

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
- Create container and enter shell (Replace PATH_TO_DATA with an absolute path):
```command
docker run --name gpuecc -it --gpus=all -p 8888:8888 --mount type=bind,source="PATH_TO_DATA",target=/workspace -w /GPU-ECC --entrypoint /bin/bash seravee08/gpuecc:latest
```
- Launch jupyter notebook:
```bash
jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --allow-root --NotebookApp.token='' --NotebookApp.password=''
```
Open your browser and navigate to: http://localhost:8888/

## Compile from source

Rquires **CUDA >= 12.6**.

### Windows 10/11
Requires **CMake 4.2.3** and **Visual Studio 2022**. Build steps:
1. In **CMake GUI**, set **Where is the source code** to the folder containing the source files and `CMakeLists.txt`  
   Example: `C:/GPU-ECC/sources`
2. Set **Where to build the binaries** to your desired build directory  
   Example: `C:/GPU-ECC/sources/build`
3. Click **Configure**
4. Click **Generate**
5. Open the generated `.sln` file in the build folder with **Visual Studio 2022**, then build the project.

### Linux
From the folder containing the source files and `Makefile`, run:

```bash
make -j
```
The executable will be generated at: build/GPU_ECC

## Citation ##
    @inproceedings{DBLP:conf/compgeom/0010W022,
      author    = {Fan Wang and
                   Hubert Wagner and
                   Chao Chen},
      editor    = {Xavier Goaoc and
                   Michael Kerber},
      title     = {{GPU} Computation of the Euler Characteristic Curve for Imaging Data},
      booktitle = {38th International Symposium on Computational Geometry, SoCG 2022,
                   June 7-10, 2022, Berlin, Germany},
      series    = {LIPIcs},
      volume    = {224},
      pages     = {64:1--64:16},
      publisher = {Schloss Dagstuhl - Leibniz-Zentrum f{\"{u}}r Informatik},
      year      = {2022},
      url       = {https://doi.org/10.4230/LIPIcs.SoCG.2022.64},
      doi       = {10.4230/LIPIcs.SoCG.2022.64},
      timestamp = {Wed, 01 Jun 2022 17:01:01 +0200},
      biburl    = {https://dblp.org/rec/conf/compgeom/0010W022.bib},
      bibsource = {dblp computer science bibliography, https://dblp.org}
      }

    @article{Wang_Wagner_Chen_2023,
      title     ={GPU computation of the Euler characteristic curve for imaging data},
      volume    ={14},
      url       ={https://jocg.org/index.php/jocg/article/view/4470},
      DOI       ={10.20382/jocg.v14i2a2},
      number    ={2}, 
      journal   ={Journal of Computational Geometry},
      author    ={Wang, Fan and Wagner, Hubert and Chen, Chao},
      year      ={2023},
      month     ={Dec.},
      pages     ={3–25}
      }
