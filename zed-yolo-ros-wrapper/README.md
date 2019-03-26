# Stereolabs ZED - YOLO 3D - ROS in C++

This package lets you use YOLO the deep learning object detector using the ZED stereo camera and the ZED SDK C++.

The detections are pre-filtered and published on a ROS topic. In the current configuration, only detections of persons are published, since this package was used for pedestrian detection. 

        /zed_yolo_detected_persons

The left image will be used to display the detected objects alongside the x, y and z position of each, using the ZED Depth and the camera coordinate system. This image is published on the ROS topic 

        /zed_yolo_detected_persons/image

## Prerequisites

- Ubuntu 16.04
- [ZED SDK](https://www.stereolabs.com/developers/) and its dependencies ([CUDA](https://developer.nvidia.com/cuda-downloads))
- OpenCV

### Build the sample with catkin

Create a catkin workspace

        mkdir -p catkin-ws/src
        cd catkin-ws
        catkin config --init --cmake-args-DCMAKE_BUILD_TYPE=RelWithDebInfo

Clone and build package

        cd src
        git clone https://github.com/PhiAbs/zed-yolo.git
        cd ..
        catkin build

## Compile Darknet

We will use a fork of darknet from @AlexeyAB : https://github.com/AlexeyAB/darknet

- It is already present in the folder libdarknet

- Simply call make in the folder

        cd libdarknet
        make -j4

- For more information regarding the compilation instructions, check the darknet Readme [here](../libdarknet/README.md)


## Run the application

### Setup the application

- Download the model file, for instance Yolov3 tiny

        wget https://pjreddie.com/media/files/yolov3-tiny.weights

### Run it

To launch the ZED with YOLO simply launch the ROS launch file

        roslaunch zed-yolo-ros-people-detector zed_yolo_people_detector.launch

In this launch file you can also adjust parameters

