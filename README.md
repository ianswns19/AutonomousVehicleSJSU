# AutonomousVehicleSJSU
Current Status of Autonomous Vehicle Build

Currently Control of DC and Servo Motors via FOCBOX VESC Working
RPLiDAR fully working along with SEN-14001 Accelerometer
RealSense Camera currently working through Modified SDK based on x86_64 adapted to ARM64, issues with getting uvc driver to work correctly fo Jetson, currently modifying Kernel
RealSense Required to Publish to Pretrained Object Detection Node

RPLIDAR SDK and REALSENSE SDK Required
Linux Kernel 28.2 for Jetson Required
CUDA 8.0 required

1. source devel/setup.bash # Use this to source development environment in order to allow launching of ros nodes
2. roslaunch racecar teleop.launch # use this command to operate the car via a controller
3. roslaunch rplidar_ros view_rplidar.launch # use this command to launch the rplidar visualization node
4. in order to demonstrate the realsense camera,rebuild sdk with modified makefile provided in folder
5. go to realsense-viewer executable located in usr/local/bin directory and double click to execute
