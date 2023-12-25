# 3D SLAM Intel Realsense D455

In this project, we used the Intel Realsense D455 Camera for 3D Slam Mapping with its integrated IMU Bosch BMI055 for Odometry data for recording the 3D SLAM data along the camera path. The video below demonstrates the recorded 3D Map view in which the pink line represents the camera's path.

video link:
https://www.youtube.com/watch?v=-xXxApcFQf8

I am using ROS Melodic in Ubuntu 18.04 on VMware Virtual Machine.

First, we need to install the following ROS Packages for using the camera
1. ROS1 wrapper for intel real sense camera (https://github.com/IntelRealSense/realsense-ros/tree/ros1-legacy)
2. sudo apt-get install ros-melodic-imu-filter-madgwick
3. sudo apt-get install ros-melodic-rtabmap-ros
4. sudo apt-get install ros-melodic-robot-localization

Run Code:
1. roslaunch realsense2_camera rs_camera.launch align_depth:=true unite_imu_method:="linear_interpolation" enable_gyro:=true enable_accel:=true
2. rosrun imu_filter_madgwick imu_filter_node _use_mag:=false _publish_tf:=false _world_frame:="enu" /imu/data_raw:=/camera/imu /imu/data:=/rtabmap/imu
3. roslaunch rtabmap_ros rtabmap.launch rtabmap_args:="--delete_db_on_start --Optimizer/GravitySigma 0.3" depth_topic:=/camera/aligned_depth_to_color/image_raw rgb_topic:=/camera/color/image_raw camera_info_topic:=/camera/color/camera_info approx_sync:=false wait_imu_to_init:=true imu_topic:=/rtabmap/imu

LinkedIn post of 3D SLAM at Michigan Technological University
https://www.linkedin.com/posts/nathir-rawashdeh-b6019428_we-were-able-to-map-the-nucor-corporation-activity-7141588559219613696-ljjI

