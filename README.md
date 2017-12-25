
# Smart Camera Car

>2017 Fall NTUEE ESlab final project 
>group members:  
>b03901004  
>b03901162 

## Before use the code

### Install OpenCV

You should install OpenCV on the Raspberry pi

Intsall cmake and some other tools

>sudo apt-get install build-essential cmake pkg-config  
>sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev  
>sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev 
>sudo apt-get install libxvidcore-dev libx264-dev 
>sudo apt-get install libgtk2.0-dev 
>sudo apt-get install libatlas-base-dev gfortran

Then clone OpenCV and contrib repository.  cd to a directory, and 

>git clone https://github.com/opencv/opencv.git 
>git clone https://github.com/opencv/opencv_contrib.git

Then make a build directory and get into it, for example:

>cd opencv 
>mkdir build 
>cd build

Then use cmake to prepare the files

>cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local  -D INSTALL_PYTHON_EXAMPLES=ON -D OPENCV_EXTRA_MODULES_PATH=&lt;opencv_contrib folder&gt;/modules &lt;opencv folder&gt;

Then compile it, use `-j4` to use 4 core of Raspberry pi.  It may takes more than 2 hours, depends on the speed of micro sd card.

>make -j4

After compile, install it

>sudo make install 
>sudo ldconfig

Then install is finish.  To save the space, you can remove the source code folders.

>sudo rm -rf opencv opencv_contrib

### Enable camera

Insert the camra module onto Raspberry pi.

Enable the camera

>sudo raspi-config

Then reboot the pi.

After rebooting, you can use `vcgencmd get_camera` to check if the camera is available.  You should see the text below:

>supported=1 detected=1

For OpenCV to use the camera, we should enable v4l2

>sudo modprobe bcm2835-v4l2

Then you can see the camera device at `/dev/video0`, and you can use `VideoCapture video(0);` to get the camera frames.


