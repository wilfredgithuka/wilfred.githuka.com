---
title: "Udacity Self Driving Car Nanodegree Term1 Project1 Finding Lane Lines"
date: 2017-07-04T07:51:33+03:00
subtitle: "To Find Lanes Lines On The Road Using Basic Computer Vision"
tags: [udacity, python, canny, OpenCV, miniconda, jupyter, numpy,]
---
![Final Image](/img/udacity/solidWhiteCurveMerged.jpg)

The main objective of this project is to find lane lines in video using basic computer vision. The lines on the road show us where the lanes are and act as a constant reference for where to steer the vehicle. Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.In this project I have created a pipeline to detect lane lines in images and videos using Python and OpenCV.

Because this is my first project I will also explain how to set up your computer and the tools required. Be warned that this post might be long, its however worth it.

## Tools
* Python3
* OpenCV
* Numpy
* Jupyter Notebook 

I have derrived this project from the Udacity's Starters Kit (below). The kit equips you with all you need to get started.

## Starter Kit

[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

The purpose of this project is to provide unified software dependency support for students enrolled in Term 1 of the [Udacity Self-Driving Car Engineer 
Nanodegree](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013).

Python 3 is used for the entirety of term 1.

There are two ways to get up and running:

### [Anaconda Environment](doc/configure_via_anaconda.md)

Get started [here](doc/configure_via_anaconda.md). More info [here](http://conda.pydata.org/docs/).

Supported Sytems: Linux (CPU), Mac (CPU), Windows (CPU)     

| Pros                         | Cons                                               |
|------------------------------|----------------------------------------------------|
| More straight-forward to use | AWS or GPU support is not built in (have to do this yourself)              |
| More community support       | Implementation is local and OS specific            |
| More heavily adopted         |                                                    |


## Objectives

* Setup python development environment with Miniconda and Jupyter Notebook
* Understand Canny Edge Detector and Hugh Transform
* Understand Numpy and OpenCV

### Installing and Configuring Miniconda(Conda)

Conda is an open source package management system and environment management system that runs on Windows, macOS and Linux. Conda quickly installs, runs and updates 
packages and their dependencies. Conda easily creates, saves, loads and switches between environments on your local computer. It was created for Python programs, but it 
can package and distribute software for any language.

Download and install miniconda then go to downloads directory on your computer and run this script
```bash
miniconda3-latest-Linux-x86_64.sh
```
#### Create Environment
This is the environment where we will be working from.

```bash
conda create -n lanedetection
```
Now lets activate our conda environment
```bash
source activate lanedetection
```
After finishing your project detactivate it using this command. Well don't deactivate it now until we are done.(But you can try if you want)
```bash
source deativate lanedetection
```

#### Configure Your New Environment

Now while inside the environment, your prompt should look like the following:
```bash
(lanedetection)[wilfred@githuka]
```
Good, now lets proceed to install the required packages
```bash
conda install -c https://conda.anaconda.org lmenpo opencv3
```
This will install 29 packages 6,604 files(16.4MB) so be patient, also install the folowing:
```bash
conda install -c asmevrer pango
```
Then run ...
```bash
pip install jupyter mousepy matplotlib
```
If you encounter and error, make sure that your linux has the folowing packages installed. Deactivate your conda environment and install them
```bash
sudo pacman -S libselinux libpng12
```
Finally to start the project, start the Jupyter Notebook
```bash
(lanedetection)[wilfred@githuka] jupyter notebook
```
## Pipeline 
In a summary the following will be our pipeline:

* Import Initial Images
* Create Helper Functions
* Load Test Images
* Convert Images to Grayscale
* Apply Gaussian Smoothing
* Apply Canny Transform
* Apply Region of interest
* Apply Hough Transform
* Merge Original Image with Lines
* Video Test

![Final Image](/img/udacity/solidWhiteCurveMerged.jpg)
This is the final image that we hope to accomplish at the end of this project.

## Approach

### Grayscale

The first step to working with our images is to convert them to grayscale. This is very importanant especially since we will be using Canny Edge Detector of OpenCV. What we are basically doing is collapsing the 3 channels of RGB into a singe channel with a pixel range of [0,255] using this code:
```python
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
![Final Image](/img/udacity/solidWhiteCurveGray.jpg)


### Solving the Yellow~White Lane Markings Problem.

Before diving straight into the Canny Edge Detector, I have realised that Yellow and White in grayscale are almost similar. Infact when you look at the above images, its certainly difficult to know which is white or yellow line. So we will convert it onto a HSV (Hue Value Saturation) HSV is the tech that enabled monochrome tvs to be able to receive colour signals. We will then apply a mask to the RGB image and return the pixels that we want.

```python
lower_yellow = np.array([20, 100, 100], dtype = “uint8”)
upper_yellow = np.array([30, 255, 255], dtype=”uint8")
mask_yellow = cv2.inRange(img_hsv, lower_yellow, upper_yellow)
mask_white = cv2.inRange(gray_image, 200, 255)
mask_yw = cv2.bitwise_or(mask_white, mask_yellow)
mask_yw_image = cv2.bitwise_and(gray_image, mask_yw)
```

We will apply a quick gaussian_blur to help us later in our Canny Edge Detector works.

```python
kernel_size = 5
gauss_gray = gaussian_blur(mask_yw_image,kernel_size)
```
So far so good :-)

### A Small Distraction

If you are fascinated by gray_image in openCV like me, here is a small python program that used openCV to apply graysc1aling to an image.

```python
import cv2
image = cv2.imread('sampleimage.png')
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
cv2.imwrite ('gray_image.png', gray_image)
cv2.imshow ('gray_image', gray_image)
cv2.waitKey (0)
cv2.destroyAllWindows()
```

## Canny Edge Detection
Simply put the Canny edge detector is an edge detection operator that uses a multi-stage algorithm to detect a wide range of edges in images. It was developed by John F. Canny in 1986. Canny also produced a computational theory of edge detection explaining why the technique works.
John Canny himself recommended a low to high threshold ratio of 1:2 or 1:3 for our canny as it computes.
```python
low_threshold = 50
    high_threshold = 150
    canny_edges = canny(gauss_gray,low_threshold,high_threshold)
```
![Final Image](/img/udacity/solidWhiteCurveCanny.jpg)
Image output with a Canny Edge Detector applied.

## Region of Interest
The region of interest is where te car will be focussing on. The last thing we want is for our car's attention to be distracted by every thing in the horizon. Everything outside the ROI will be blacked out to zero. Here is the snipet of code that does all the heavylifting...
```python
def maskAction(img):
    ysize = img.shape[0]
    xsize = img.shape[1]
    region = np.array([ [0, ysize], [xsize/2,(ysize/2)+ 10], [xsize,ysize] ], np.int32)
    return region_of_interest(img, [region])

testImagesMasked = doSaveAndDisplay(testImagesCanny, 'test_images_region', testImageNames, maskAction)
```
![Final Image](/img/udacity/solidWhiteCurveRegion.jpg)
Image output with a ROI defined. This is what the car will concentrate on.

## Hough Transform
The Hough transform is a technique which can be used to isolate features of a particular shape within an image.Hough transform is most commonly used for the detection of regular curves such as lines, circles, ellipses, etc.

The big take away is that in XY space lines are lines and points are points, but in Hough space lines correspond to points in XY space and points correspond to lines in XY space. This is what our pipeline will look like:

* Pixels are considered points in XY space.
* ```python hough_lines() ``` transforms these points into lines inside of Hough space.
* Wherever these lines intersect, there is a point of intersection in Hough space.
* The point of intersection corresponds to a line in XY space. Thanks @galen.ballew

![Final Image](/img/udacity/solidWhiteCurveHough.jpg)
Image output with Hough Transform applied

## Merging Original Image with Lines
Now we plug in our original image with the Lines, this is what I got...

![Final Image](/img/udacity/solidWhiteCurveMerged.jpg)
Nice :-)

## How about Video?
We can also try it out on video, have a look below..

### Original Video
https://youtu.be/3WvcvB6xS9I

### Processed Video
https://youtu.be/1AXc-F-idEU

## Conclusion

This project has actually introduced me into the deeper powers of python and computer vision. I still have an urge to use my own local images in this project. Thats for next time. 

All the files for this project can be found in the [repo](https://github.com/wilfredgithuka/usdcnd-project1-lane-detection)



