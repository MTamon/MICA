<h2 align="center"><b>MICA - Towards Metrical Reconstruction of Human Faces</b></h2>

<h4 align="center"><b><a href="https://zielon.github.io/" target="_blank">Wojciech Zielonka</a>, <a href="https://sites.google.com/site/bolkartt/" target="_blank">Timo Bolkart</a>, <a href="https://justusthies.github.io/" target="_blank">Justus Thies</a></b></h4>

<h6 align="center"><i>Max Planck Institute for Intelligent Systems, Tübingen, Germany</i></h6>

<h4 align="center">
<a href="https://youtu.be/vzzEbvv08VA" target="_blank">Video&nbsp</a>
<a href="https://arxiv.org/pdf/2204.06607.pdf" target="_blank">Paper&nbsp</a>
<a href="https://zielon.github.io/mica/" target="_blank">Project Website&nbsp</a>
<a href="https://github.com/Zielon/metrical-tracker" target="_blank">Face Tracker&nbsp</a>
<a href="https://github.com/Zielon/MICA/tree/master/datasets/" target="_blank"><b>Dataset&nbsp</b></a>
<a href="https://keeper.mpdl.mpg.de/f/6b12c44378e64738b993/" target="_blank">Supplemental&nbsp</a>
<a href="mailto:&#109;&#105;&#099;&#097;&#064;&#116;&#117;&#101;&#046;&#109;&#112;&#103;&#046;&#100;&#101;">Email</a>
</h4>

<div align="center"> 
<img src="documents/teaser.jpg">
<i style="font-size: 1.05em;">Official Repository for ECCV 2022 paper Towards Metrical Reconstruction of Human Faces</i>
</div>
<br>

<div align="center"> 
&#x26A0 The face tracker is now available under <a href="https://github.com/Zielon/metrical-tracker" target="_blank">Metrical Photometric Tracker&nbsp</a> &#x26A0
</div>

### Installation

#### Supported environment (CUDA 12.8 branch)

| Component    | Version                                               |
|--------------|-------------------------------------------------------|
| OS           | Ubuntu 22.04                                          |
| Python       | 3.11                                                  |
| PyTorch      | 2.9.1 (torchvision 0.24.1)                            |
| CUDA Toolkit | 12.8                                                  |
| GCC          | gcc-11 / g++-11                                       |
| GPU arch     | sm_75, sm_80, sm_86, sm_89, sm_90, sm_120             |

The dependency set is aligned with
[MTamon/FlashAvatar @ release/cuda128-fixed](https://github.com/MTamon/FlashAvatar/tree/release/cuda128-fixed)
and [MTamon/DECA @ release/cuda128](https://github.com/MTamon/DECA/tree/release/cuda128).

#### Quick install (recommended)

```shell
git clone https://github.com/MTamon/MICA.git
cd MICA
python3.11 -m venv .venv
source .venv/bin/activate
./install_128.sh   # pins + chumpy (git) + pytorch3d v0.7.8 source build
./install.sh       # downloads FLAME2020 + MICA + insightface models
```

`install_128.sh` installs the pinned library set from `requirements_128.txt`
(torch 2.9.1 + CUDA 12.8 wheels), builds `chumpy` from its numpy 2.x-friendly
main branch, and source-builds `pytorch3d` v0.7.8 against the new torch.

`install.sh` is the original data-download script; it still asks for your
FLAME credentials and fetches the MICA / insightface model bundles. The conda
`environment.yml` path is retained only for reference and is no longer
actively maintained on this branch.

#### Legacy (CUDA 11.6 / PyTorch 1.13) install

The original conda recipe is still in `environment.yml` for reproducibility:

```shell
./install.sh   # original path: downloads models + `conda env create -f environment.yml`
```

you will be asked to provide `{flame_user}` and `{flame_password}` for your FLAME account in order to access the file server.

### Pre-trained Models

If you decide to not use the installation script, the pretrained model can be found under the [link](https://drive.google.com/file/d/1bYsI_spptzyuFmfLYqYkcJA6GZWZViNt/view?usp=sharing). After downloading, please place it in the `/data/pretrained/mica.tar` location. Additionally, you will need to provide models for `inisghtface`:
1) [antelopev2](https://drive.google.com/file/d/16PWKI_RjjbE4_kqpElG-YFqe8FpXjads/view?usp=sharing)
2) [buffalo_l](https://drive.google.com/file/d/1navJMy0DTr1_DHjLWu1i48owCPvXWfYc/view?usp=sharing)

then you need to unzip them and place in `~/.insightface/models/`. The `install.sh` script does it for you.

### How To Use

To use MICA you can simply run the `demo.py` file. It will process all the images from `demo/input/` folder and create the output destination for each subject with `.ply` mesh, rendered image, and `.npy` FLAME parameters.

### Dataset and Training

The MICA dataset consists of eight smaller datasets for about 2300 subjects under a common FLAME topology. Read more information about how to obtain and use it under the [link](https://github.com/Zielon/MICA/tree/master/datasets/). To train MICA the images from all eight datasets are needed. The repository contains scripts how to generate the Arcface input images as well as the complete list of all the images used for the training. More information can be found [here](https://github.com/Zielon/MICA/tree/master/datasets).

When you train from scratch for Arcface model initialization please download [Glint360K](https://github.com/deepinsight/insightface/tree/master/recognition/arcface_torch) and specify the path to it in the config as `cfg.model.arcface_pretrained_model`.

### Testing

The testing was done using two datasets, [Stirling](http://pics.stir.ac.uk/ESRC/) and [NoW](https://now.is.tue.mpg.de/). In the [model folder](https://github.com/Zielon/MICA/tree/master/models) you can find the corresponding scripts to run testing routine, which generates the meshes. To calculate the NoW challenge error you can use the following [repository](https://github.com/soubhiksanyal/now_evaluation).   

### Citation
If you use this project in your research please cite MICA:
```bibtex
@proceedings{zielonka22mica,
  author = {Zielonka, Wojciech and Bolkart, Timo and Thies, Justus},
  title = {Towards Metrical Reconstruction of Human Faces},
  journal = {European Conference on Computer Vision},
  year = {2022}
}
```
