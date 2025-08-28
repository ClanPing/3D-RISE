# 3D-RISE
[ELSP2025] 3D Reconstruction, Integration, Segmentation, and Editing (3D-RISE) to revolutionize construction site simulations.

| [Paper](https://www.elspub.com/papers/j/1893818303650844672) |

<p align="center">
<img src="assets/graphical_abstract.png" alt="Workflow Overview" width="700"/>
</p>

The 3D-RISE workflow is designed to revolutionize construction site simulations by enabling high-quality, editable 3D environments for construction site layout planning and simulation training.

This project utilizes 3D Gaussian Splatting (3DGS) as the core reconstruction technique, transforming captured image datasets into realistic and computationally efficient 3D scenes.

To enhance and customize these reconstructions, 3D-RISE integrates these powerful open-source repositories:

- [SAGA (Segment Any 3D GAussians)](https://github.com/Jumpat/SegAnyGAussians)
- [SuGaR (Surface-Aligned Gaussian Splatting)](https://github.com/Anttwo/SuGaR/tree/main?tab=readme-ov-file)
- [XScene-UEPlugin (Unreal Engine 5 3DGS plugins)](https://github.com/xverse-engine/XScene-UEPlugin)

By combining these tools, 3D-RISE allows the generation of customizable 3D construction sites where individual components can be segmented, refined and reused for simulation workflows. The outcome is a pipeline that bridges raw 3D reconstruction and practical applications in the Architecture, Engineering, and Construction (AEC) industry.

## Installation
### Requirements

Ran in Ubuntu 22.04.

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
