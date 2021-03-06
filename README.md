# aruco_ros
This repository is about detection of markers i.e. Aruco markers / April tags based on ROS
The following are the steps to get started.

![screenshot from 2016-12-29 18 48 33](https://cloud.githubusercontent.com/assets/23419376/21954443/d77a9af2-da76-11e6-8343-2b3c6a384a44.png)

![screenshot from 2017-01-14 16 33 13](https://cloud.githubusercontent.com/assets/23419376/21954468/7dffb10a-da77-11e6-9345-98427e3e175e.png)


1. Download the aruco library from http://www.uco.es/investiga/grupos/ava/node/26 
    I've used the aruco library version of 2.0.14.  
	
2. Once you have downloaded the library, extract and buildit using the following steps  
    a. $ cd Downloads/aruco-2.0.14  
    b. $ mkdir build  
    c. $ cd build  
    d. $ cmake ..  
    e. $ make  
    f. $ sudo make install  
    The install location /usr/local should be remembered for future use.
	
3. Download an aruco marker/ April tag and print it.

4. Follow the following steps  
    a. $ cd catkin_ws/src  
    b. clone this repository  https://github.com/shashankvkt/aruco_ros  
    c. $ source /opt/ros/YOUR_DISTRIBUTION/setup.bash  
    d. $ cd ..  
    e. $ catkin_make --pkg ros_aruco -DARUCO_PATH=/usr/local  
	
5. If you are using a monocular / stereo camera for detection of markers clone the following repository in the catkin source directory - https://github.com/ayushgaud/usb_cam  
give the path of your calibration files accordingly

6. Connect the camera to the usb port and run the following commands

    a. $ roslaunch usb_cam stereo_cam-test.launch (for stereo camera)  / $ roslaunch usb_cam usb_cam-test.launch (monocular)
	
          Incase of issues change the launch file accordingly.
    b. Run the image_proc node as    $ ROS_NAMESPACE=stereo rosrun stereo_image_proc stereo_image_proc (change it accordingly for           monocular one) on another tab (Ctrl+Shift+T)  
    c. $ rosrun ros_aruco ros_aruco - on another tab
	
        Running this node will enable detection of marker and will print the centre and 'z' pose of the tag.  
    d. If you want to get the depth from disparity of the marker using stereo camera, then on a new tab,  
	
        i. $ cd catkin_ws/src/ros_aruco/src  
        ii. $ python ros_aruco_stereo.py  
        This command will get you the depth from disparity using the formula  Z = (f*T)/D,
            where f = focal length, T = baseline, D=disparity and Z = depth.  

7. Lastly,the data of the pose of the marker and it's centre, is published as a ROS Topic, so that further development can be made using the data.  
	a. /aruco/centre/pose - gives the centre of the marker  
	b. /aruco/linear/pose - gives the orientation and pose of the marker w.r.t camera  

