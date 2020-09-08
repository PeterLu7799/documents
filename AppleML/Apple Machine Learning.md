# Apple's Machine Learning

## Porpose

* The performance of the device has been enhanced.
* iOS 14 added several new features


## Outlines

* Going through all the ML features that Apple provided so far. 
* Introducing some core features


## Computer Vision

<img src="./Images/Models_so_far.png" width = "600" align=center />

## Core ML

### What does Core ML provide

* Run models fully on-device
* Convert models to Core ML
* Run advanced neural networks
* Personalize models on-device
* Deploy models by CloudKit
* Encrypt models

### Architecture

<img src="./Images/coreml_level.png" width = "600" align=center />

* [BNNS](https://developer.apple.com/documentation/accelerate/bnns) is the subset of Accelerate framework, it provides a collection of functions that you use to construct neural networks for training and inference via CPU's vector processor

* [Metal Performance Shaders](https://developer.apple.com/documentation/metalperformanceshaders)

### Models

* Core ML Models
* Create ML
* Turi Create
* Core ML Tools
* Metal Performance Shaders (MPS)

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

Use the coremltools Python package to convert models from third-party training libraries such as TensorFlow and PyTorch to the Core ML format.

* [github](https://github.com/apple/coremltools)

<img src="./Images/coremltools.png" width = "600" align=center />

#### Metal Performance Shaders (MPS)

* MPS Graph (iOS 14)[WWDC2020](https://developer.apple.com/videos/play/wwdc2020/10677/)



## Vision

Some outstanding features:

* Face detection
* Face landmark
* Image Registration
* Hand Pose (iOS 14)

<img src="./Images/hand_landmarks.png" width = "600" align=center />

* Body Pose (iOS 14)

<img src="./Images/VisionPoseJoints.png" width = "600" align=center />

* Trajectory detection (iOS 14)

<img src="./Images/trajectoryDetect.png" width = "500" align=center />

* Contour detection (iOS 14)

<img src="./Images/contour.png" width = "300" align=center />

* Optical Flow (iOS 14)

Analyze the movement bwtween two frames, and tell how each pixel flow in X and Y

<img src="./Images/OpticalFlow.png" width = "300" align=center />


## Natural Language

The Natural Language framework provides a variety of natural language processing (NLP) functionality with support for many different languages and scripts. 

* [Tokenization](https://developer.apple.com/documentation/naturallanguage/tokenizing_natural_language_text)
	* Breaking up a piece of text into linguistic units or tokens such as words, sentences and paragraphs.
* [Language Identification](https://developer.apple.com/documentation/naturallanguage/identifying_the_language_in_text)
	* Automatically detecting the language of a piece of text.
* Linguistic Tags
	* [Identifying Parts of Speech,](https://developer.apple.com/documentation/naturallanguage/identifying_parts_of_speech) classify nouns, verbs, adjectives, and other parts of speech in a string.
	* [Named entity recognition](https://developer.apple.com/documentation/naturallanguage/identifying_people_places_and_organizations), identifying tokens as names of people, places, or organizations.
* Text Embedding
	* [Finding Similarities Between Pieces of Text.](https://developer.apple.com/documentation/naturallanguage/finding_similarities_between_pieces_of_text)
* Natural Language Models by Create ML
	* Custom word tagging
	* Custom text classification



## Speech

## Sound

## Core Image
* Scaling
* Morphology Operations

To make small features in your image more prominent

* Noise Reduction
* Edge Detection
* Contrast enhance
* Binarization
* Comparing images
* Re-generating barcodes

## Alternatives

* Tensorflow Lite
* Pytorch Mobile

