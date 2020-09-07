# Apple's Machine Learning

## Porpose

* The performance of the device has been enhanced.
* iOS 14 added several new features


## Outlines

* Going through all the ML features that Apple provided so far. 
* Introducing some core features


## Computer Vision

![Models](images/Models_so_far.png)

## Core ML

### What does Core ML provide

* Run models fully on-device
* Convert models to Core ML
* Run advanced neural networks
* Personalize models on-device
* Deploy models by CloudKit
* Encrypt models

### Architecture

![](images/coreml_level.png)

* [BNNS](https://developer.apple.com/documentation/accelerate/bnns) is the subset of Accelerate framework, it provides a collection of functions that you use to construct neural networks for training and inference via CPU's vector processor

* [Metal Performance Shaders](https://developer.apple.com/documentation/metalperformanceshaders)

### Models

* Core ML Models
* Create ML
* Core ML Tools
* Turi Create

#### Core ML Models

The following popular models are provided by Apple in its [website](https://developer.apple.com/machine-learning/models/) so far.

* FCRN-DepthPrediction
* MNIST
* UpdatableDrawingClassifier
* MobileNetV2
* Resnet50
* SqueezeNet
* DeeplabV3
* YOLOv3
* YOLOv3-Tiny
* PoseNet
* BERT-SQuAD

#### Create ML

Create machine learning models for use in your app.

* Create Core ML models
* Model previews
* On-device training
* eGPU training support

##### Provide Model types 

* Image
	* Image classification
	* Object detection
	* Style transfer

* Video
	* Action classification [WWDC video](https://developer.apple.com/videos/play/wwdc2020/10043/)
		it is also a classification task and powered by body pose estimation and Human body actions
	* Style transfer 

* Motion
	* Activity classification

* Sound
	* Sound classfication

* Text
	* Text classification
	* Word tagging

* Tabular
	* Tabular classification
	* Tabular regression
	* Recommendation

#### Turi Create

Apple provides a open source toolkits for creating Core ML models via Python.

* [Documentation](https://apple.github.io/turicreate/docs/userguide/)
* [Github](https://github.com/apple/turicreate#documentation)

##### Supported ML scenarios 

* Recommender Systems
* Image Classification
* Drawing Classification
* Sound Classification
* Image Similarity
* Object Detection
* One-Shot Object Detection
* Style Transfer
* Activity Classifier
* Text Classifier

##### Machine learning essentials

* Classifiers
* Regression
* Graph analytics
* Clustering
* Nearest Neighbors
* Topic models

#### Core ML Tools

![](images/coremltools.png)

[github](https://github.com/apple/coremltools)

## Vision

Some outstanding features:

* Face detection
* Face landmark
* Image Registration
* Hand Pose (iOS 14)

<img src="./images/hand_landmarks.png" width = "600" align=center />

* Body Pose (iOS 14)

![](images/VisionPoseJoints.png)

* Trajectory detection (iOS 14)

![](images/trajectoryDetect.png)

* Contour detection (iOS 14)

![](images/contour.png)

* Optical Flow (iOS 14)


## Natural Language

## Speech

## Sound

## Core Image
### Scaling
### Morphology Operations

To make small features in your image more prominent

### Noise Reduction
### Edge Detection
### Contrast enhance
### Binarization
### Comparing images
### Re-generating barcodes


## Alternatives

* Tensorflow Lite
* Pytorch Mobile
