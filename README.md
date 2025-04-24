# Front-Loader-Capstone-Project
# Code for HSV colorspace filter
sudo apt update
sudo apt install ros-$ROS_DISTRO-orbbec-camera ros-$ROS_DISTRO-cv-bridge ros-$ROS_DISTRO-vision-opencv

# Clone the Orbbec ROS2 SDK if needed
cd ~/ros2_ws/src/  # Change to your workspace if different
git clone https://github.com/orbbec/OrbbecSDK_ROS2.git
cd ~/ros2_ws
colcon build --symlink-install
source install/setup.bash

# Start the camera node
ros2 launch orbbec_camera femto_bolt.launch.py

# In a new terminal, start RViz2
ros2 run rviz2 rviz2

cd ~/ros2_ws/src
ros2 pkg create --build-type ament_python color_tracker --dependencies rclpy sensor_msgs cv_bridge geometry_msgs

# Place the script in the appropriate folder
cp color_tracker_ros2.py ~/ros2_ws/src/color_tracker/color_tracker/color_tracker_node.py

# update packages setup.py
entry_points={
    'console_scripts': [
        'color_tracker = color_tracker.color_tracker_node:main',
    ],
},

# In Terminal 1
ros2 launch orbbec_camera femto_bolt.launch.py

# In Terminal 2
ros2 run color_tracker yellow_tracker
