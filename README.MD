# ENGG*3130 Final Project
# Improving consistencey of object segmentation in video using FlowNet2 
### By: Spencer Ploeger (0969141, sploeger@uoguelph.ca)
### Lucas Dasovic (0963516, ldasovic@uoguelph.ca)

Detectron2 is a computer vision framework based on pytorch. It can use many different models to perform object detection and segmentation, keypoint detection, panoptic segmentation, etc. It is very good at performing these tasks on single images, but major inconsistencies are introduced when attmepting to perform the same tasks on video. This is becasue the models Detectron2 is trained on are all based on single frame datasets. When predictions are made on videos, they are done as though the video is simply a list of independent frames.

Issues arise because there is no notion or connectiveness between frames. This results in random artifacting in frames casued by changes in light, contrast, etc. whichs makes Detectron2 to temporarily and falsely detect objects that only dissapear very quickly afterwards. This inconsistencey is undesirable.

To attempt to correct this, FlowNet2-Pytorch is used to create a new ground-truth layer for training Detectron2. It gives a layer of moving objects frame-to-frame. We can use this to create a loss function and attempt to re-train Detectron2.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites and Installation

1. Install conda using its [installation guide](https://docs.conda.io/projects/conda/en/latest/user-guide/install/)

2. Install the conda environment from the included ```environment.yml``` file.
Run:
```conda env create -f environment.yml```. The environment is called ```project-master```

4. Activate the conda environment with ```conda activate project-master```

3. Install detectron2 using its [installation guide](https://github.com/facebookresearch/detectron2/blob/master/INSTALL.md)

4. From this [google drive link](https://drive.google.com/drive/folders/1qXZd8nObw84jSYklAFjNnH6djVymr65N?usp=sharing), download all the folders into the root directory of your project. **Note: You can press "Download All" from google drive and then unzip into your project directory**

Your file tree should look like this when complete (from root directory):

```
.
├── configs
│   ├── Base-RCNN-C4.yaml
│   └── COCO-InstanceSegmentation
│       └── mask_rcnn_R_50_C4_1x.yaml
├── environment.yml
├── Final_Notebook_v2.ipynb
├── flow_data
│   ├── driveby
│   │   ├── 000000.flo
│   │   ├── 000001.flo
│   │   │   ..........
│   │   ├── 000028.flo
│   │   ├── 000029.flo
│   │   └── images
│   │       ├── 000000.flo.png
│   │       ├── 000001.flo.png
│   │       │   ..........
│   │       ├── 000028.flo.png
│   │       └── 000029.flo.png
│   ├── driving_on_401
│   │   ├── 000000.flo
│   │   ├── 000001.flo
│   │   │   ..........
│   │   ├── 000028.flo
│   │   ├── 000029.flo
│   │   └── images
│   │       ├── 000000.flo.png
│   │       ├── 000001.flo.png
│   │       │   ..........
│   │       ├── 000028.flo.png
│   │       └── 000029.flo.png
│   └── walking
│       ├── 000000.flo
│       ├── 000001.flo
│       │   ..........
│       ├── 000028.flo
│       ├── 000029.flo
│       └── images
│           ├── 000000.flo.png
│           ├── 000001.flo.png
│           │   ..........
│           ├── 000028.flo.png
│           └── 000029.flo.png
├── models
│   ├── __init__.py
│   ├── mobilenet.py
│   ├── model_final_9243eb.pkl
│   ├── __pycache__
│   │   ├── __init__.cpython-38.pyc
│   │   ├── mobilenet.cpython-38.pyc
│   │   └── resnet.cpython-38.pyc
│   └── resnet.py
├── notebook_supporting
│   └── scale.png
├── README.MD
├── sample_images
│   └── VOC
│       ├── 2007_004189.jpg
│       ├── 2007_004189.png
│       ├── 2007_006449.png
│       ├── 2008_002536.jpg
│       ├── 2008_002536.png
│       ├── 2010_005582.jpg
│       ├── 2010_005582.png
│       └── car.png
├── sample_videos
│   ├── driveby.mp4
│   ├── driving_on_401.mp4
│   └── walking.mp4
└── utils
    ├── cmap.npy
    ├── cs_cmap.npy
    ├── helpers.py
    ├── __init__.py
    ├── layer_factory.py
    └── __pycache__
```


## Built With

* [Detectron2](https://github.com/facebookresearch/detectron2) - To generate segmentation masks
* [Lightweight refinent](https://github.com/DrSleep/light-weight-refinenet) - To generate segmentation masks
* [PyTorch](https://pytorch.org/) - An open source machine learning framework
* [FlowNet2](https://github.com/dancelogue/flownet2-pytorch) - Used to create flow masks
 

## Authors

* **Spencer Ploeger** - *Initial work*



## Acknowledgments

* Thor. Thor literally spent hours with me this semster, and has taght me so much about ML, CV, and python in general. Thank you!!!

