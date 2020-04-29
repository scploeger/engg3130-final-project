# ENGG*3130 Final Project
# Improving consistencey of object segmentation in video using FlowNet2 
### By: Spencer Ploeger (0969141, sploeger@uoguelph.ca)
### Lucas Dasovic ()

Detectron2 is a computer vision framework based on pytorch. It can use many different models to perform object detection and segmentation, keypoint detection, panoptic segmentation, etc. It is very good at performing these tasks on single images, but major inconsistencies are introduced when attmepting to perform the same tasks on video. This is becasue the models Detectron2 is trained on are all based on single frame datasets. When predictions are made on videos, they are done as though the video is simply a list of independent frames.

Issues arise because there is no notion or connectiveness between frames. This results in random artifacting in frames casued by changes in light, contrast, etc. whichs makes Detectron2 to temporarily and falsely detect objects that only dissapear very quickly afterwards. This inconsistencey is undesirable.

To attempt to correct this, FlowNet2-Pytorch is used to create a new ground-truth layer for training Detectron2. It gives a layer of moving objects frame-to-frame. We can use this to create a loss function and attempt to re-train Detectron2.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

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
├── Final_Notebook.ipynb
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
│   │   ├── 000000.flo
│   │   ├── 000001.flo
│   │   │   ..........
│   │   ├── 000028.flo
│   │   ├── 000029.flo
│       └── images
│   │       ├── 000000.flo.png
│   │       ├── 000001.flo.png
│   │       │   ..........
│   │       ├── 000028.flo.png
│   │       └── 000029.flo.png
├── models
│   └── model_final_9243eb.pkl
├── notebook_supporting
│   └── scale.png
├── README.MD
└── sample_videos
    ├── driveby.mp4
    ├── driving_on_401.mp4
    └── walking.mp4


```

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
