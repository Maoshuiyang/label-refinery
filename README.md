## Label Refinery: *Improving ImageNet Classification through Label Progression*
By [Hessam Bagherinezhad](http://homes.cs.washington.edu/~hessam/),
[Maxwell Horton](http://homes.cs.washington.edu/~mchorton/),
[Mohammad Rastegari](http://www.umiacs.umd.edu/~mrastega/),
and [Ali Farhadi](http://homes.cs.washington.edu/~ali/).

### Introduction

This is a pytorch training script that can be used to train image classifier on
ImageNet. The purpose of this repository is to back the experimental results
presented in the Label Refinery paper. The Label Refinery paper is
[published on arxiv](https://arxiv.org/abs/1805.02641).

Label Refinery is a training mechanism that can be used to train any
classification model. Label Refinery improves the quality of the labels, and
therefore the quality of the models trained with those labels. Using Label
Refinery improves the state-of-the-art accuracy of a variety of network
architectures:

Model          | Paper Number :: Top-1 | Our Impl. :: Top-1  | Label Refinery :: Top-1
-------------- |:---------------------:|:-------------------:|:-----------------------:
AlexNet        | 59.3                  | 57.93               | **66.28**
MobileNet      | 70.6                  | 68.53               | **73.39**
MobileNet0.75  | 68.4                  | 65.93               | **70.92**
MobileNet0.5   | 63.7                  | 63.03               | **66.66**
MobileNet0.25  | 50.6                  | 50.65               | **54.62**
ResNet-50      | N/A                   | 75.7                | **76.5**
ResNet-34      | N/A                   | 73.39               | **75.06**
ResNet-18      | N/A                   | 69.7                | **72.52**
ResNetXnor-50  | N/A                   | 63.1                | **70.34**
VGG-16         | 73                    | 70.1                | **75**
VGG-19         | 72.7                  | 71.39               | **75.46**
Darknet19      | 72.9                  | 70.6                | **74.47**

For complete list of results and some analysis, please refer to
[our paper](https://arxiv.org/abs/1805.02641).

### Usage
#### Prerequisite
To use this source code you need Python3.5+, a copy of ImageNet 2012 dataset,
and a few python3 packages. A full set of python dependencies is listed in
[requirements.txt](requirements.txt) for cuda 8 users. If you're not using cuda,
or using a different version of cuda, change `torch==0.4.0` line to your desired
pytorch 0.4 wheel url. You can install them all through pip3:
```
pip3 install -r requirements.txt
```

#### Train models

You can train models either with the standard labels, or with the refined
labels. To train `AlexNet` with the standard labels:
```
./train.py --model AlexNet --imagenet /path/to/imagenet2012
```
To train `AlexNet` with refined labels generated by a trained `AlexNet` Label
Refinery:
```
./train.py --model AlexNet --imagenet /path/to/imagenet2012 --label-refinery-model AlexNet --label-refinery-state-file /path/to/trained/alexnet.pytar
```

#### Test models

To test a trained AlexNet model:
```
./test.py --model AlexNet --model-state-file /path/to/alexnet.pytar --imagenet /path/to/imagenet2012
```


#### Pre-trained weights

Model                | Description                                           | Top-1  | Link
-------------------- |:-----------------------------------------------------:|:------:|:------:
`AlexNet^1`            | AlexNet trained with standard labels.               | 57.93  | [get](https://storage.googleapis.com/xnorai-public/downloads/label-refinery/alexnet%5E1.pytar)
`AlexNet^2`            | AlexNet trained with labels refined by `AlexNet^1`. | 59.97  | [get](https://storage.googleapis.com/xnorai-public/downloads/label-refinery/alexnet%5E2.pytar)
`AlexNet^3`            | AlexNet trained with labels refined by `AlexNet^2`. | 60.87  | [get](https://storage.googleapis.com/xnorai-public/downloads/label-refinery/alexnet%5E3.pytar)
`AlexNet^4`            | AlexNet trained with labels refined by `AlexNet^3`. | 61.22  | [get](https://storage.googleapis.com/xnorai-public/downloads/label-refinery/alexnet%5E4.pytar)
`AlexNet^5`            | AlexNet trained with labels refined by `AlexNet^4`. | 61.37  | [get](https://storage.googleapis.com/xnorai-public/downloads/label-refinery/alexnet%5E5.pytar)
`AlexNet By ResNet-50` | AlexNet trained with labels refined by `ResNet-50`. | 66.28  | [get](https://storage.googleapis.com/xnorai-public/downloads/label-refinery/alexnet-from-resnet50.pytar)
`ResNet-50`            | ResNet-50 trained with standard labels.             | 75.7   | [get](https://storage.googleapis.com/xnorai-public/downloads/label-refinery/resnet50.pytar)

#### License
By downloading this software you acknowledge that you read and agreed all the
terms in the `LICENSE` file.
