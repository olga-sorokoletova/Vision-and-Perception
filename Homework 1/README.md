# Image Processing

This is the repository of the first homework proposed for the course of *Vision and Perception*.

It contains solutions of four exercises intended to master skills in Image Processing:
1. Feature Detection and Description
2.
3.
4.

Code implementations (in Python) for all of them are collected in the [scripts](https://github.com/olga-sorokoletova/Vision-and-Perception/tree/main/Homework%201/scripts) folder.

## Assignment 1: Feature Detection and Description

### Task Assignment

Starting from the Bag of Visual Words algorithm with SIFT, implement Harris Feature Extractor and another method at your choice. Compare SIFT with Harris and SIFT with the new method. Report the features extraction phase and discuss the results. Show the extracted features using the three different methods on sample image from the dataset. Furthermore, the three confusion matrices as output of the BOW algorithm must be provided.

### Implementation

#### Jupyter Notebook

[```feature_detection_and_description.ipynb```](https://github.com/olga-sorokoletova/Vision-and-Perception/blob/main/Homework%201/scripts/feature_detection_and_description.ipynb)

#### Pre-processing

Decision to work in a gray-scale has been taken to reach consistency between methods since ```cv2.cornerHarris()``` functions takes as input images in a gray-scale. Images are resized to the (150, 150) dimension.

#### Harris

Since Harris is just a Feature Extractor, but combining of it with the SIFT Descriptor is not desirable, another approach has been developed – Descriptor List is filled directly with the extracted and refined corners (Open-CV tutorial recommends function ```cv2.cornerSubPix()``` which refines the corners detected with sub-pixel accuracy. For this we pass the centroids of the Harris corners and have to define the criteria when to stop the iteration).

#### BRISK

The method implemented as a method at choice was BRISK (Binary Robust Invariant Scalable Key points). BRISK has a handmade sampling pattern. Gaussian filter is applied to different regions separately. Additionally, threshold distinguishes patterns into short, long and unused pairs. Wherein, short hand
distance pairs are used to compute intensity values, whereas long hand distance pairs are used to find orientation. BRISK, as well as SIFT, contains both Detector and Descriptor, and is provided with the same methods to call.

### Results

#### Comment
Extracted features for the randomly sampled from the dataset and pre-processed image are shown below and can be found in the [```feature_detection_and_description.ipynb```](https://github.com/olga-sorokoletova/Vision-and-Perception/blob/main/Homework%201/scripts/feature_detection_and_description.ipynb) as well as confusion matrices and other information regarding to
performance of the methods. In the sense of the training time, Harris is the fastest method (1-1.5 mins), although it is influenced by the absence of the descriptors computation after extracting Harris corners. Training time of the BRISK is compatible with the one of SIFT, but in general the later one executes faster (8 vs 5 mins), despite of the fact that BRISK is considered to be a high-speed method, meanwhile SIFT – the method of a moderate speed. Probably, that’s a matter of this particular dataset. From the point of view of the properties, both BRISK and SIFT are invariant to the translation, but BRISK performs better for view point change. On the given Dataset in average SIFT reaches about 0.5-0.6 value of accuracy, BRISK – 0.4-0.5, and Harris – 0.3-0.4. As could be seen from the confusion matrices, Harris stably is able to recognize at some level cities and faces, doing some work on the recognizing of the offices and house buildings, but is not able to tell anything about some other classes. In particular, it has problems with images, semantics of which is not well-defined by the corners, e.g. sea or green, or with images, for which corner features are not that useful fordistinguishing because of similarity of the corner patterns between the classes, e.g. house indoor has approximately equal probabilities to be identified as house indoor, city, office or house building. But house indoor is a problematic category for all of the three algorithms and so further work
over improvements should be first of all focused on this aspect. In other categories, both BRISK and SIFT keep more ”uniform” distribution of guesses, but it is noticeable that SIFT performs generally better, and the reason is seen on the sampled image: BRISK tends to ignore border areas of an image. SIFT approves it’s robustness to shifts/translations/any spatial modifications and performs the best on the given Dataset, but precise investigation of
the SIFT’s results on the sampled images shows a weak ability to handle orientation and illumination.

## Author

- Olga Sorokoletova - 1937430

