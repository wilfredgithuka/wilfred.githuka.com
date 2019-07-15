---
title: "A Baby Steps Introduction Into Convolutional Neural Networks - The Missing Manual"
date: 2017-08-08T15:36:47+03:00
subtitle: "A Gentle Introduction into CNN, LeNet and OpenCV with Python 3"
tags: [Python, CNN, LeNet, Kernel, ComputerVision, OpenCV]
draft: true
---
In machine learning, a convolutional neural network (CNN, or ConvNet) is a class of deep, feed-forward artificial neural network that have successfully been applied to analyzing visual imagery.CNNs use relatively little pre-processing compared to other image classification algorithms. This means that the network learns the filters that in traditional algorithms were hand-engineered. This independence from prior knowledge and human effort in feature design is a major advantage.

A CNN consists of an input and an output layer, as well as multiple hidden layers. The hidden layers are either convolutional, pooling or fully connected.

The convolutional layer is the core building block of a CNN. The layer's parameters consist of a set of learnable filters (or kernels), which have a small receptive field, but extend through the full depth of the input volume. During the forward pass, each filter is convolved across the width and height of the input volume, computing the dot product between the entries of the filter and the input and producing a 2-dimensional activation map of that filter. As a result, the network learns filters that activate when it detects some specific type of feature at some spatial position in the input.

The LeNet architecture was first introduced by LeCun et al. in their 1998 paper, Gradient-Based Learning Applied to Document Recognition. As the name of the paper suggests, the authors’ implementation of LeNet was used primarily for OCR and character recognition in documents.

The LeNet architecture is straightforward and small, (in terms of memory footprint), making it perfect for teaching the basics of CNNs — it can even run on the CPU (if your system does not have a suitable GPU), making it a great “first CNN”.

However, if you do have GPU support and can access your GPU via Keras, you will enjoy extremely fast training times (in the order of 3-10 seconds per epoch, depending on your GPU).

# Reference
* [Wikipedia - Convolutional neural network](https://en.wikipedia.org/wiki/Convolutional_neural_network)
* [LeNet – Convolutional Neural Network in Python](http://www.pyimagesearch.com/2016/08/01/lenet-convolutional-neural-network-in-python/)
