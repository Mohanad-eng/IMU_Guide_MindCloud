# IMU_Guide_MindCloud
repo for imu 

to install 

make a ws and inside the src :

``git clone https://github.com/flynneva/bno055``

**For Runinng the IMU bno005 on the laptop**

``ros2 launch bno055 bno055.launch.py ``

then **run a static transform**

``ros2 run tf2_ros static_transform_publisher 0 0 0 0 0 0 base_link bno055``

then to simulate in rviz install **imu plugin**,

``sudo apt install ros-jazzy-rviz-imu-plugin``

why ?

because rviz want to know where the imu with rescprect to the world 

the previous command means that :

“The IMU is mounted on the robot at the center, no offset”

base_link ------> bno005

where did i get the fixed frame ?

``ros2 topic echo /bno055/imu``

in the part Fixed_frame 

you will see the bno055

``
header:
  stamp:
    sec: 1777481525
    nanosec: 335376422
  frame_id: bno055
orientation:
  x: -0.007019262438977776
  y: -0.06604210399107786
  z: -0.029847124631827242
  w: 0.9973456369817119
orientation_covariance:
- 0.0159
- 0.0
- 0.0
- 0.0
- 0.0159
- 0.0
- 0.0
- 0.0
- 0.0159
angular_velocity:
  x: 0.0
  y: 0.0
  z: 0.0
angular_velocity_covariance:
- 0.04
- 0.0
- 0.0
- 0.0
- 0.04
- 0.0
- 0.0
- 0.0
- 0.04
linear_acceleration:
  x: -0.16
  y: 0.0
  z: 0.0
linear_acceleration_covariance:
- 0.017
- 0.0
- 0.0
- 0.0
- 0.017
- 0.0
- 0.0
- 0.0
- 0.017
---

``

