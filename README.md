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

In a typical Coriolis MEMS gyroscope, a vibrating proof mass is attached to a reference frame

They utilize the Coriolis effect, where an oscillating mass, when rotated, experiences a perpendicular force proportional to the rotation speed. This force causes tiny deflections in the vibrating element, which are detected as capacitance changes by capacitive-sensing structures and converted into a digital signal. 


3- A magnetometer is a device that measures the **magnetic field, including its strength and orientation.**

![](<https://www.jouav.com/wp-content/uploads/2023/11/magnetometers-imu-1024x724.jpg>)


then the **MCU** Fuse all this and gives us **orientation**


**the old vs modren IMU's** :

here is photos of some moduels

![](<https://www.jouav.com/wp-content/uploads/2023/11/components-of-inertial-measurement-unit.jpg>)

this is the old imu that the gyro,accleo,magno are seperated

![](<https://cdn11.bigcommerce.com/s-2fbyfnm8ev/images/stencil/1280x1280/products/901/3153/apiqazhk3__12576.1548549983__38456.1586537929.jpg?c=2>)

the square chip in the middle inside it all 3 sensors

![the chip that contains all three](<https://cdn-shop.adafruit.com/970x728/5158-02.jpg>)

the chip shape

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

here is the **rviz** :
![](<Screenshot from 2026-04-30 14-59-49.png>)

**Let's see the imu messeage :**

``

---
header:
  stamp:
    sec: 366
    nanosec: 784000000
  frame_id: imu_link
orientation:
  x: -0.4339462411720465
  y: 0.9009383994952168
  z: -0.00041946711093343396
  w: -0.0006957980971923171
orientation_covariance:
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
angular_velocity:
  x: 0.0
  y: 0.0
  z: -3.552850267281465e-15
angular_velocity_covariance:
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
linear_acceleration:
  x: 0.01584333326663922
  y: -0.0014936324077541314
  z: -9.808398344311744
linear_acceleration_covariance:
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
- 0.0
---

``

