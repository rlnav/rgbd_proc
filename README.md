# RGB-D Data Processing

Tools to process RGB-D data collected from the
[Hiwonder Tracked Robot](https://www.hiwonder.com/products/suspended-shock-absorbing-tracked-chassis?variant=40378709835863) equipped with
[Luxonis OAK-D lite](https://shop.luxonis.com/products/oak-d-lite-1) depth camera.

## Installation

The package is organized as a
[ROS 2](https://docs.ros.org/) package and can be installed using the following commands:

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
git clone git@github.com:rlnav/rgbd_proc.git
cd ~/ros2_ws/
rosdep install --from-path src --ignore-src -r
colcon build --symlink-install --packages-select rgbd_proc
```

### USB rules

For the OAK camera to be recognized by Ubuntu, you must set the udev rules. Ensure you are using a USB 3.0 cable and port.

```bash
echo 'SUBSYSTEM=="usb", ATTRS{idVendor}=="03e7", MODE="0666"' | sudo tee /etc/udev/rules.d/80-movidius.rules
sudo udevadm control --reload-rules && sudo udevadm trigger
```

## Usage

Launching depthai camera driver:
```bash
ros2 launch depthai_ros_driver_v3 driver.launch.py
```

Launching depthai camera driver in RGBD configuration:
```bash
ros2 launch depthai_ros_driver_v3 rgbd_pcl.launch.py
```

Launching depthai camera driver in RGBD configuration with RTAB-Map SLAM:
```bash
ros2 launch depthai_ros_driver_v3 rtabmap.launch.py
```

Reference: [Luxonis DepthAI ROS driver](https://docs.luxonis.com/software-v3/depthai/ros/driver/) docs.