# AutonomousVehicleSJSU
Current Status of Autonomous Vehicle Build
RealSense Camera Unable to publish to ROS Node
RPLiDAR able to Publish to ROSCORE and Send Point Data for Processing
ROSCORE can succesfully send signals to the VESC which sends the necessary signals to the DC and Servo Motors
SEN-14001 Accelerometer sending acceleration and tilt Data to Jetson
Currently Control of DC and Servo Motors via FOCBOX VESC Working
Unable to Publish to Pretrained DNN Object Detection Node without

The main problems that we have encountered were getting all the devices to properly interface with the NVIDIA Jetson, mainly because even though they were all compatible with ROS and had their own ROS libraries, 
they were not necessarily compatible with the Jetson since the RealSense Camera and the RPLiDAR were both incompatible with the ARM64 architecture. While the issue with the RPLiDAR was resolved and the LiDAR was 
able to successfully publish data to the ROS Core, the RealSense Camera became the major issue and continues to be an issue since even though the SDK Makefile was able to be modified to allow the SDK for 
LibRealsense 2.0 to be installed, the UVC driver still needs to be patched since it requires an updated realsense version to function correctly but the patch is unable to work since it is also incompatible with 
the ARM64 architecture. We have tried many different workarounds that others have found, however they have not removed the errors since after some examination of the underying file structure our system is different 
enough that the workarounds are ineffective.

We were able to get all the peripherals sending or receiving data from the ROS Core on the Jetson except for the RealSense Camera. The FOCBOX VESC is able to receive the necessary signals from the Jetson in order
to send the correct Electrical Signals to the DC and Servo Motors. The LiDAR is able to send point Data to the Jetson which can then be further processed into useful information for the ROS Core. The RealSense Camera
is able to send image data to the Jetson but is unable to then transfer that data to the ROS Core which as a result is impeding any progress.

Linux Kernel 28.2 for Jetson Required
1. Download Jetpack 3.2.1 onto Host Linux Machine
2. Connect Jetson to Host Linux Machine via Ethernet Bridge
3. Follow setup steps and specify connection via Ethernet Bridge in Jetpack installer
4. Specify Full Install and Accept all EULAs, then follow all the steps to set Jetson into recovery mode
CUDA 8.0 required
1. Download Jetpack 3.1 onto Host Linux Machine
2. Connect Hetson to Host Linux Machine via Ethernet Bridge
3. Follow setup steps and specify connection via Ethernet Bridge in Jetpack installer
4. Specify Custom Install and Accept EULA for CUDA, then follow all the steps to set Jetson into recovery mode
RPLIDAR SDK and REALSENSE SDK Required
1. Unpack directories for RPLIDAR SDK and REALSENSE SDK and move them out of the containing folder into the home directory
2. Run Makefile in REALSENSE SDK
   - COMMAND: $ make
Unpack ROS directory and move to home directory - change catkin workspace to racecar-ws
Make sure to run a catkin make inside of racecar-ws directory

Setting Up ROS environment
COMMAND: $ source devel/setup.bash # Use this to source development environment in order to allow launching of ros nodes
Running Teleoperation Demo of Car- Allows for operation of the car via an external control source in order to allow the
functionality of the DC and Servo Motors to be tested.
COMMAND: $ roslaunch racecar teleop.launch # use this command to operate the car via a controller
Running visualisation of LiDAR Data - Provides a visual representation of the points generated by the 2D LiDAR which allows
for insight into the sensitivity of the device and allows for on the fly tuning of parameters
COMMAND: $ roslaunch rplidar_ros view_rplidar.launch # use this command to launch the rplidar visualization node
Running RealSense Visualisation Via SDK, options can be changed inside of GUI which can switch between stereoscopic and 
infrared views
- go to realsense-viewer executable located in usr/local/bin directory and double click to execute
