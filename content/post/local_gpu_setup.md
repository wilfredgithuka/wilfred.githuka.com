---
title:       "Setting Up A Local Deep Learnning Environment NVIDIA GPU+Tensorflow+Keras+CuDNN+CUDA in Archlinux"
subtitle:    "How to setup a local Linux-Based Deep Learning Environment in Anaconda"
description: ""
date:        2019-02-26
author:      "Wilfred Githuka"
image:       "/img/deep_learning.jpg"
tags:        ["self-driving", "deep-learning"]
categories:  ["Linux" ]
---
Dont get me wrong, am not against cloud based GPU's designed to simplyfy the process of training your
neural networks but sometimes having a local less powerful setup is great. An AWS GPU is awesome and
is less tiring when it comes to setup, so this manual is for those who want to get to low level
and understand what happens there.

### Machine Specs
First let me list my hardware specs so that we can have a benchark as we go forth.

* OS: Archlinux
* CPU: Intel Core i7
* Speed: 3488.27 Mhz
* Clock: 99.79 Mhz
* Memory: 16,384 Mb
* GPU: GeForce GTX 1050 rev a1

### Nvidia Drivers, CUDA and CuDNN Installation

According to Nvidia, the Deep Neural Network library (cuDNN) is a GPU-accelerated library of primitives 
for deep neural networks. cuDNN provides highly tuned implementations for standard routines such as 
forward and backward convolution, pooling, normalization, and activation layers. CUDA on the other hand
is NVIDIA's programming langauge for its GPU's.

There are tons of manuals online for installing the above but I will make mine as simple as possible.

First Install Nvidia's drivers

```console
sudo pacman -S nvidia nvidia-utils
```
Then install CUDA and CuDNN

```console
sudo pacman -S cuda cudnn
```
Test the installation of CuDNN

```console
sudo cp /opt/cuda/* /home/wilfred
cd samples/
sudo make
cd bin/x86_64/linux/release
./deviceQuerry
RESULT = PASS
```
One you get a RESULT=PASS then the installation was successful. Clean up unwante files using this 
command

```console
cd ~
rm -rf samples
```
### Anaconda

You can choose between the large anaconda or a smaller miniconda. I choose the larger one. Note that
this installation shall take up loads of time. Anaconda is 3.4GB and shall be installed in /opt/anaconda

```console
yay -S anaconda
echo 'export PATH = "/opt/anaconda/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Test the anaconda installation.

```console
anaconda --version
```

It will show the installed version of anaonda.

### Create a Custom Deep Learning Environment

Next we shall create a custon deep learning environment which we shall be using for various tasks.

```console
conda create -n deep-learning
```
Then list to check whether the environment has been created.

```console
conda list
```

Now activate our new environment

```console
source activate deep-learning
```
Install pip, python's package manager to our environment

```console
conda install pip
```

At this point, stop and check the versions of python and pip. As at the time of this writing, you should get
something like: python 3.7.2 and pip 19.0.1

Now install Tensorflow GPU. This will take sometime.

```console
sudo pip install tensorflow-gpu
```
Check too the installed version of tensorflow. 1.13 rc2

Check to see that tensorflow has been installed correctly by running the following command.

```console
python -c "import tensorflow as tf; tf.enable_eager_execution(); print(tf.reduce_sum(tf.random_normal([1000, 1000])))"
```
Once you see the result showing the GPU's properties. It was a successful installation.

At this point we can install the basic tools for a deep learning environment. These will be around 78MB and are
installed by conda. Some shall require root so adding a sudo conda install xxx will do.

```console
sudo conda install numpy matplotlib jupyter pillow scikit-learn scikit-image scipy h5py flask python-socketio seaborn pandas ffmpeg imageio pyqt
```
The next step is to install other tools using python's pip

```console
sudo pip install moviepy opencv-python requests keras eventlet
```
You are now ready to work on your local GPU for deep learning.

Back to code...
