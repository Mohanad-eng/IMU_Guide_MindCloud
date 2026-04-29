## First what is imu ?
----------------------------------------------------------------------

**imu** An IMU (Inertial Measurement Unit) is an electronic device that measures and reports a body's specific force, angular rate, and sometimes the orientation of the body using a combination of accelerometers, gyroscopes, and sometimes magnetometers.

In robotics, mobile phones, drones, and autonomous vehicles, the IMU is one of the most fundamental sensors — it is the device that tells the system "how am I moving right now?" without needing any external reference like GPS or a camera.

it is classified to :

1- 6-DOF means it contains 3-DOF Accelerometer, 3-DOF Gyroscope 

| Sensor | DOF | Measures |
|---|---|---|
| Accelerometer | 3-DOF (x, y, z) | Linear force / acceleration |
| Gyroscope | 3-DOF (roll, pitch, yaw rate) | Angular velocity |


2- 9-DOF means it contains 3-DOF Accelerometer,3-DOF Gyroscope ,3-DOF Magnetometer

| Sensor | DOF | Measures |
|---|---|---|
| Accelerometer | 3-DOF (x, y, z) | Linear force / acceleration |
| Gyroscope | 3-DOF (roll, pitch, yaw rate) | Angular velocity |
| Magnetometer | 3-DOF (x, y, z) | Earth's magnetic field |

The magnetometer acts like a digital compass — it measures Earth's magnetic field to provide an **absolute heading reference**. 

This corrects the gyroscope's heading drift by always knowing which direction is magnetic North.

 
**Common 9-DOF chips:** BNO055(our module), MPU-9250, ICM-42688-P, LSM9DS1

![](<https://www.amazon.in/Adafruit-Absolute-Orientation-Fusion-Breakout/dp/B017PEIGIG>)

-------------------------------------------------------

**to install :**

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

