# Installing-Tensorflow-object-detection-API-on-Pi-3

This was forked from https://www.theta.co.nz/news-blogs/tech-blog/object-detection-on-a-raspberry-pi/

Some alterations where relevant as I did this from a fresh install on Pi. You may need to reduce the split amount of ram used by the GPU 
temporarily in case there are issues with memory resources during the install using:

sudo raspi-config > then go to 'advanced' > memory split and set it to 16MB.
(change it back to 64MB after its running)

This is the easiest way to get TensorFlow onto your Raspberry Pi 3. I have personally tested this only on Python 3.4.

Note that currently, the pre-built binary is targeted for Raspberry Pi 3 running Raspbian 8.0 ("Jessie"), so this may or may not work for you. 

The specific OS release is the following:

Raspbian 8.0 "Jessie"
Release: March 2, 2017
Installed via NOOBS 2.3

First, install the dependencies for TensorFlow:

sudo apt-get update

# For Python 2.7

sudo apt-get install python-pip python-dev

# For Python 3.4+

sudo apt-get install python3-pip python3-dev


Next, download the wheel file from this repository and install it:

# For Python 2.7

wget https://github.com/samjabrahams/tensorflow-on-raspberry-pi/releases/download/v1.1.0/tensorflow-1.1.0-cp27-none-linux_armv7l.whl

sudo pip install tensorflow-1.1.0-cp27-none-linux_armv7l.whl

# For Python 3.4

wget https://github.com/samjabrahams/tensorflow-on-raspberry-pi/releases/download/v1.1.0/tensorflow-1.1.0-cp34-cp34m-linux_armv7l.whl

sudo pip3 install tensorflow-1.1.0-cp34-cp34m-linux_armv7l.whl

Finally, we need to reinstall the mock library to keep it from throwing an error when we import TensorFlow:

# For Python 2.7

sudo pip uninstall mock

sudo pip install mock

# For Python 3.4+

sudo pip3 uninstall mock

sudo pip3 install mock

# Object Detection API

Object detection comes as part of the official Tensorflow research models.  Its purpose is to detect multiple objects in single images.  

Clone this repository somewhere handy:

git clone https://github.com/tensorflow/models.git

Detailed installation instructions and troubleshooting for the Object Detection API can be found here.

We need a variety of libraries to run object detection, so we first need to install all of these:

pip3 install --upgrade pip

sudo apt-get install protobuf-compiler

sudo pip3 install pillow

sudo apt-get install python3-lxml

sudo pip3 install jupyter

sudo pip3 install matplotlib


We now need to compile the Object Detection API using Protobuf. Navigate to your tensorflow/models/research/ directory, and run the following:

sudo protoc object_detection/protos/*.proto --python_out=.

slim has moved into the research directory in the repo. To get it to work I had to do:

export PYTHONPATH=/home/username/models/research/slim:$PYTHONPATH

python3 object_detection/builders/model_builder_test.py
