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

## BibteX

If you find this project helpful for your research, pleasure consider citing the report and giving a ⭐.
```
@article{Chai2025_SC_0019,
  author  = {Chai, P. and Hou, L. and Lo, X. and Zhang, G. and Chen, H. and others},
  title   = {Revolutionising construction site simulations with automated 3D segmentation and mesh construction},
  journal = {Smart Construction},
  year    = {2025},
  doi     = {10.55092/sc20250019},
  url     = {https://doi.org/10.55092/sc20250019}
}
```

## Acknowledgement

The implementation of 3D-RISE heavily refers to [Gaussian Splatting](https://github.com/graphdeco-inria/gaussian-splatting), [SAGA](https://github.com/Jumpat/SegAnyGAussians), [SuGaR](https://github.com/Anttwo/SuGaR), [XScene-UEPlugin](https://github.com/xverse-engine/XScene-UEPlugin) and we sincerely thank them for their contributions in making this research project successful. We also gratefully acknowledge computational resource grants through [RMIT AWS Supercomputing Hub (RACE HUB)](https://www.rmit.edu.au/partner/hubs/race).

## Requirements

Ran in Ubuntu 22.04.

The software requirements are the following:

- Conda (recommended for easy setups)
- C++ Compiler for PyTorch extensions
- CUDA toolkit 11.8 for PyTorch extensions
- C++ Compiler and CUDA SDK must be compatible
- FFMPEG for frames extractions from video datasets
- COLMAP for camera poses estimation from images

Please refer to the original [3D Gaussian Splatting repository](https://github.com/graphdeco-inria/gaussian-splatting) for more details about requirements.

## Installation

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

## Prepare data

`datasets` folder contains excavator, sign, structures to be used in this project. You can also use your own custom dataset.

To convert a video to images, make sure to install `ffmpeg` and run the following command:
```bash
# Install ffmpeg
sudo apt upate
sudo apt install -y ffmpeg

# Execute command
ffmpeg -i <Path to the video file> -qscale:v 1 -qmin 1 -vf fps=<FPS> %04d.jpg
```
where `<FPS>` is the desired sampling rate of the video images. An FPS value of 1 corresponds to sampling one image per second. We recommend to adjust the sampling rate to the length of the video, so that the number of sampled images is between 100 and 300.

Dataset structure below is required for COLMAP camera poses estimation:
```
<location>
|---input
	|---<image 0>
	|---<image 1>
	|---...
|---<path to the video file>
```

Make sure to install `colmap` and run:
```bash
# Install colmap
sudo apt update
sudo apt install -y colmap

# Execute command
python convert.py -s <location>
```

The expected dataset structure is as follows:
```
<location>
|---images
|   |---<image 0>
|   |---<image 1>
|   |---...
|---sparse
    |---0
        |---cameras.bin
        |---images.bin
        |---points3D.bin
|---run-colmap-geometric.sh
|---run-colmap-photometric.sh
|---<path to the video file>
```

## 3D segmentation

<p align="center">
  <img src="assets/excavator.jpg" height="150" alt="excavator JPG">
  &nbsp;&nbsp;&nbsp;&nbsp;
  <img src="assets/excavator.gif" height="150" alt="excavator OBJ">
</p>

Please refer to the original [SAGA repository](https://github.com/Jumpat/SegAnyGAussians) for more detailed instructions.

Download the pretrained [public ViT-H model](https://dl.fbaipublicfiles.com/segment_anything/sam_vit_h_4b8939.pth) for Segment Anything Model (SAM). The downloaded model path will be referred as `<path to the pre-trained SAM model>` in the following commands ahead.
