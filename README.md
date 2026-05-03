# First what is imu ?

![](<https://www.seeedstudio.com/blog/wp-content/uploads/2020/01/imu-sensor-guide.png>)


**imu** An IMU (Inertial Measurement Unit) is an electronic device that measures and reports a body's specific force, angular rate, and sometimes the orientation of the body using a combination of accelerometers, gyroscopes, and sometimes magnetometers.

In robotics, mobile phones, drones, and autonomous vehicles, the IMU is one of the most fundamental sensors — it is the device that tells the system "how am I moving right now?" without needing any external reference like GPS or a camera.

### it is classified to :

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

 
**Common 9-DOF chips:** BNO055(our module), MPU-9250, ICM-42688-P, LSM9DS1
![](<>)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**IMU components :**

1-Accelerometers :

Accelerometers, the nifty devices that gauge and relay specific forces, come in a variety of flavors, including mechanical, quartz, and MEMS accelerometers.

In IMUs, the accelerometers often use MEMS technology, which stands for microelectromechanical systems.

These accelerometers have a tiny mass connected to a reference system by a spring.

This setup allows them to measure how fast something is speeding up or slowing down.

They keep track of the mass's movement using capacitors, and special electronic components.

When the accelerometer is not moving, the mass creates a specific capacitance, like a baseline, showing no acceleration.

But when there's acceleration, the mass moves, and this changes the capacitance.

![](<https://www.jouav.com/wp-content/uploads/2023/11/accelerometers-imu.gif>)

so, the Accelerometer measures the **Linear acceleration + gravity**

2- Gyroscopes :

Gyroscopes in an IMU measure **angular velocity**, indicating how fast and in what direction something is rotating.

In a typical Coriolis MEMS gyroscope, a vibrating proof mass is attached to a reference frame, inducing a secondary vibration perpendicular to the drive axis when rotated.

This secondary vibration sensed through changes in capacitance, provides a signal proportional to the Coriolis force and the sensed rotation.


3- A magnetometer is a device that measures the **magnetic field, including its strength and orientation.**

then the **MCU** Fuse all this and gives us **orientation**


**the old vs modren IMU's** :

![](<https://www.jouav.com/wp-content/uploads/2023/11/components-of-inertial-measurement-unit.jpg>)

this is the old imu that the gyro,accleo,magno are seperated

![](<https://cdn11.bigcommerce.com/s-2fbyfnm8ev/images/stencil/1280x1280/products/901/3153/apiqazhk3__12576.1548549983__38456.1586537929.jpg?c=2>)

the square chip in the middle inside it all 3 sensors

![](<https://cdn-shop.adafruit.com/970x728/5158-02.jpg>)

------------------------------------------------------------------------------------------------------------------------------------------------------------------

**to install the official package :**

make a ws and inside the src :

``git clone https://github.com/flynneva/bno055``


**For Runinng the IMU bno005 on the laptop**


``ros2 launch bno055 bno055.launch.py ``


then to simulate in rviz install **imu plugin** :


``sudo apt install ros-jazzy-rviz-imu-plugin``


then **run a static transform** :


``ros2 run tf2_ros static_transform_publisher 0 0 0 0 0 0 base_link bno055``

why ?

because rviz want to know where the **imu with rescprect to the world** 


the previous command means that :


“The IMU is mounted on the robot at the center, no offset”


**base_link ------> bno005**


where did i get the fixed frame ?

``ros2 topic echo /bno055/imu``

in the part Fixed_frame 

you will see the bno055

``

header:
  stamp:
    sec: 1777481525  (**the time sensor take**)
    nanosec: 335376422 
  frame_id: bno055 (**frame of the sensor**)
orientation: (**quatrenuion readings for the rotations**)
  x: -0.007019262438977776
  y: -0.06604210399107786
  z: -0.029847124631827242
  w: 0.9973456369817119
orientation_covariance: (**the covariance that tell us how confideint the readings**)
- 0.0159
- 0.0
- 0.0
- 0.0
- 0.0159
- 0.0
- 0.0
- 0.0
- 0.0159
angular_velocity: (**angular velocity from the magenometer**)
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
linear_acceleration: (**linear from gyro**)
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

