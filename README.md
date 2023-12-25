# 3D_SLAM_Intel_Realsense_D455
3D Slam Mapping using Intel Realsense D455 Camera

I am using Ubuntu 18.04 for ROS Melodic 

First, we need to install the following ROS Packages for using the camera
1. ROS1 wrapper for intel real sense camera (https://github.com/IntelRealSense/realsense-ros/tree/ros1-legacy)
2. sudo apt-get install ros-melodic-imu-filter-madgwick
3. sudo apt-get install ros-melodic-rtabmap-ros
4. sudo apt-get install ros-melodic-robot-localization


Run Code:
1. roslaunch realsense2_camera rs_camera.launch align_depth:=true unite_imu_method:="linear_interpolation" enable_gyro:=true enable_accel:=true
2. rosrun imu_filter_madgwick imu_filter_node _use_mag:=false _publish_tf:=false _world_frame:="enu" /imu/data_raw:=/camera/imu /imu/data:=/rtabmap/imu
3. roslaunch rtabmap_ros rtabmap.launch rtabmap_args:="--delete_db_on_start --Optimizer/GravitySigma 0.3" depth_topic:=/camera/aligned_depth_to_color/image_raw rgb_topic:=/camera/color/image_raw camera_info_topic:=/camera/color/camera_info approx_sync:=false wait_imu_to_init:=true imu_topic:=/rtabmap/imu

Below is the LinkedIn post of 3D SLAM at Michigan Technological University
https://www.linkedin.com/posts/nathir-rawashdeh-b6019428_we-were-able-to-map-the-nucor-corporation-activity-7141588559219613696-ljjI?utm_source=share&utm_medium=member_desktop
