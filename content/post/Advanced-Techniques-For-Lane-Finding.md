---
title: "Advanced Techniques for Lane Finding In Autonomous Vehicles"
date: 2018-03-31T06:57:54Z
subtitle: "Some more complex OpenCV tools for Image Analysis"
tags: [udacity, OpenCV]
draft: true
---

When building a self driving car or an autonomous vehicle, 80% of the hard work is the perception. If my earler post about Computer Vision I used simple algorithims to detect lane lines when a car is driving on a road. In this post I will be going deeper to make an algo that can handle curves and changes in distance as the car moves. Also I will cover how to detect other vehicles on the road so that our vehicle does not just change lanes without checking if there are other vehicles on the desitination lane which can cause an accident.

This whole post will be dicided into two parts:

* Advanced Lane Finding
* Vehicle Detection and Tracking

### Correcting Image Distortion
Image distortion occurs when a camera looks at 3D objects in the real world and transforms them into a 2D image, this transformation isn’t perfect. Distortion actually changes what the shape and size of these 3D objects appear to be. Distortion can change the apparent size of an object in an image. It can change the apparent shape of an object in an image. It can also cause an object's appearance to change depending on where it is in the field of view. Finally it can make objects appear closer or farther away than they actually are.

#### Finding Corners In A Chessboard Image Using OpenCV
In this example we are going to use 2 key openCV functions to count how many corbers are there in a chessboard image. By corners here I mean the points where black and white intersect.

```python
import numpy as np
import cv2
import matplotlib.pyplot as plt
import matplotlib.image as mpimg

# prepare object points
nx = 8 #number of inside corners in x
ny = 6 #number of inside corners in y

# Make a list of calibration images
fname = 'calibration_test.png'
img = cv2.imread(fname)

# Convert to image to grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Find the chessboard corners
ret, corners = cv2.findChessboardCorners(gray, (nx, ny), None)

# If found, draw corners
if ret == True:
    # Draw and display the corners
    cv2.drawChessboardCorners(img, (nx, ny), corners, ret)
    plt.imshow(img)

```

![Chessboard-Distorted-Image](/img/udacity/chessboard-distorted.jpg)

#### Challenge: How to Callibrate Your Camera
If you're up for a challenge, go ahead and try these steps on your own camera images. Just print out a chessboard pattern, stick it to a flat surface, and take 20 or 30 pictures of it. Make sure to take pictures of the pattern over the entire field of view of your camera, particularly near the edges.

To extract object points and image points you can check out the Jupyter notebook in this repository. If you're following along with the code in the notebook, be sure you set the right size for your chessboard, the link above is to a 9 x 6 pattern, while before we were using an 8 x 6.

### Perspective Transform
In perspective transform we change the values of Z so that we get a bird's eye view of the road. This helps because ultimately we want to measure the curvature of the lines, and to do that we need to transform to a top-down view. Road images are taken using a front facing camera which will have some objects appearing smaller as you move away from the camera.

#### Exercise: Undistort and Transform Perspective
The main objective of this exercise is to find corners, calliberate my camera, undstort an image and apply a perspective transform. This preety much summarises the above concepts altogether. I will feed it an image with a chessboard which is distorted. It will oputput an undistorted image and a  wrapped image. The function should be able to:

* Undistort the image using cv2.undistort() with mtx and dist
* Convert to grayscale
* Find the chessboard corners
* Draw corners
* Define 4 source points (the outer 4 corners detected in the chessboard pattern)
* Define 4 destination points (must be listed in the same order as src points!)
* Use cv2.getPerspectiveTransform() to get M, the transform matrix
* use cv2.warpPerspective() to apply M and warp your image to a top-down view

#### Code

import pickle
import cv2
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.image as mpimg

Read in the saved camera matrix and distortion coefficients
These are the arrays you calculated using cv2.calibrateCamera()

dist_pickle = pickle.load( open( "wide_dist_pickle.p", "rb" ) )
mtx = dist_pickle["mtx"]
dist = dist_pickle["dist"]

Read in an image

img = cv2.imread('test_image2.png')
nx = 8 # the number of inside corners in x
ny = 6 # the number of inside corners in y

def corners_unwarp(img, nx, ny, mtx, dist):
    undist = cv2.undistort(img, mtx, dist, None, mtx)
    # Convert undistorted image to grayscale
    gray = cv2.cvtColor(undist, cv2.COLOR_BGR2GRAY)
    # Search for corners in the grayscaled image
    ret, corners = cv2.findChessboardCorners(gray, (nx, ny), None)
    
    if ret == True:
    # If we find any corners, we draw them
        cv2.drawChessboardCorners(undist, (nx, ny), corners, ret)
        offset = 100
        img_size = (gray.shape[1], gray.shape[0])
        src = np.float32([corners[0], corners[nx-1], corners[-1], corners[-nx]])
        dst = np.float32([[offset, offset], [img_size[0]-offset, offset], 
                                        [img_size[0]-offset, img_size[1]-offset], 
                                        [offset, img_size[1]-offset]])
        M = cv2.getPerspectiveTransform(src, dst)
        warped = cv2.warpPerspective(undist, M, img_size)
    return warped, M

top_down, perspective_M = corners_unwarp(img, nx, ny, mtx, dist)
f, (ax1, ax2) = plt.subplots(1, 2, figsize=(24, 9))
f.tight_layout()
ax1.imshow(img)
ax1.set_title('Original Image', fontsize=50)
ax2.imshow(top_down)
ax2.set_title('Undistorted and Warped Image', fontsize=50)
plt.subplots_adjust(left=0., right=1, top=0.9, bottom=0.)

#### Explanation
The cod is divided into 3 parts:
* Reading the image
* Function
* Display

### Sobel Operator
The Sobel operator is at the heart of the Canny edge detection algorithm. Sobel operators with a kernel size of 3 (implying a 3 x 3 operator in each case). This is the minimum size, but the kernel size can be any odd number. A larger kernel implies taking the gradient over a larger region of the image, or, in other words, a smoother gradient.

#### Applying Sobel
