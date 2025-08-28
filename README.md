# 3D-RISE
[ELSP2025] 3D Reconstruction, Integration, Segmentation, and Editing (3D-RISE) to revolutionize construction site simulations.
| [Paper](https://www.elspub.com/papers/j/1893818303650844672) |

Abstract: *The construction industry requires dynamic and realistic site simulations for effective site layout planning (SLP) and safety training. This paper introduces 3-Dimensional Reconstruction, Integration, Segmentation, and Editing (3D-RISE), a novel workflow integrating 3D Gaussian Splatting (3DGS), Segment Any 3D Gaussians (SAGA), and Surface-Aligned Gaussian Splatting for Efficient 3D Mesh Reconstruction and High-Quality Mesh Rendering (SuGaR) to create customisable and high-quality 3D construction scenes. The workflow leverages advanced segmentation and mesh reconstruction techniques to generate editable models while maintaining scene realism. Evaluation metrics from the initial 3DGS outputs across three image datasets (namely, steel structure, excavator, and random model) demonstrate the effectiveness of the pipeline, achieving peak signal-to-noise ratio (PSNR) values of 22.984, 35.254, and 25.854, respectively, after 30K iterations. The structural similarity index measure (SSIM) scores ranged from 0.783 to 0.951, highlighting the workflow’s ability to generate visually accurate outputs. Despite its robust capabilities, 3D-RISE has limitations, including reliance on datasets with 360-degree coverage, the inability to directly modify 3DGS-rendered scenes in Unreal Engine (UE) version 5.3, and a high demand for computational power. Running 3D-RISE on GPUs with lower specifications significantly increases processing time, requiring optimisation through downsampling or lower iteration counts, which may affect output quality. Future work focuses on integrating generative artificial intelligence (AI) to generate 3D-ready models from single images, reducing dataset requirements and computational overhead while improving scalability.*
## Installation
### Requirements

The software requirements are the following:

- Conda (recommended for easy setups)
- C++ Compiler for PyTorch extensions
- CUDA toolkit 11.8 for PyTorch extensions
- C++ Compiler and CUDA SDK must be compatible

Please refer to the original [3D Gaussian Splatting](https://github.com/graphdeco-inria/gaussian-splatting) repository for more details about requirements.

### Installation

Start by cloning this repository:
```bash
git clone https://github.com/ClanPing/3D-RISE.git
```

Then fetch required submodules:
```bash
cd 3D-RISE
git submodule update --init -- SuGaR SAGA third_party/kmeans_pytorch third_party/segment-anything
```

Next, install the dependencies:
```bash
conda env create -f environment.yml
conda activate 3drise
```
