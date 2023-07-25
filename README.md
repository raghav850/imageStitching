# Image stitching using opencv_contrib library

## Getting Started

The opencv contrib library must first be installed on the computer; a link to it is provided below. The IDE must then be configured such that the linker is aware of any external references used in the library.

### IMPORTANT: make sure the solution platform is set to x64 architecture, as the opencv is build on x64, otherwise the solution won't build.


## Algorithm


The algorithm's objective is to take two photos having a "common" region and combine them into a single image. The user must input the photographs in sequence, with the left image coming up first and the right image coming up second, even if it may be simpler for the human eye to recognize this matching. This sequence demonstrates the existence of a common zone that the user is aware of, but it also shows that two photos may be inputted that do not share a common region and nonetheless constitute a series. The algorithm is ineffective here.


There are some steps followed in order to implement the stitching algorithm:

* ### Use the SURF technique to find the KeyPoints in a picture.

A well-liked technique utilized in the opencv package, the SURF approach is used to find the KeyPoints. A *hessian threshold* is used to identify the keypoints. Lowering the threshold will allow you to see more keypoints in a picture.


* ### Calculating descriptors

The descriptors are calculated and retrieved based on the prior KeyPoints discovered using the same SURF approach.


* ### FLANN Matching

The Fast Library for Approximate Nearest Neighbors, or FLANN, determines which local picture characteristics have the greatest matches. Based on the picture descriptors, those matches are determined. After obtaining those matches, a filter must be applied to them: the distance between the matches must be three times the minimum distance.


* ### Using the RANSAC approach, determine the homography between two planes.


A generic method for parameter estimation that can deal with a high percentage of outliers in the input data is called RANDOM SAmple Consensus (RANSAC). RANSAC essentially makes approximations based on the input values that are the most "good"; the values that are "odd" are excluded.


* [Overview of the RANSAC algorithm.](http://www.cse.yorku.ca/~kosta/CompVis_Notes/ransac.pdf)
* [RANSAC explained.](http://www.cs.tau.ac.il/~turkel/imagepapers/RANSAC4Dummies.pdf)


We locate the homography matrix, a 3x3 mask, via approximation using the RANSAC approach. The purpose of homography is to rotate a given image to match another image seen from a different angle.


* [Basic concepts of the homography explained with code.](https://docs.opencv.org/master/d9/dab/tutorial_homography.html)


## Acknowledged errors

The method only functions if the user submits two images that meet the requirements: the two images represent a sequence, thus they share a common region, and they are correctly inputted; the first image must be the one on the left, and the second image must be the one on the right. The outcome is not what is wanted if this description is not met.


## Resources and references

[Image Panorama Stitching with OpenCV](https://towardsdatascience.com/image-panorama-stitching-with-opencv-2402bde6b46c)

[Image Stitching with OpenCV](https://www.pyimagesearch.com/2018/12/17/image-stitching-with-opencv-and-python/)

