##      📔 HOMEWORK 2
This repository has been created in order to fulfill the second homework of RoboticsLab 2024/2025 class. 

## 💻 Usage 
###      🔨 Build
First of all, clone this repo in your ros2_ws/src folder
```
git clone https://github.com/PasFar/Homework-2.git
```
Then, build the packages using the following command inside the ros2_ws folder and source the setup.bash file 
```
colcon build
. install/setup.bash
```
### ✅ How to run
Now you can run the nodes. You have different options.

 To test torque controlled trajectories you can use:
   ```
ros2 launch iiwa_bringup iiwa.launch.py command_interface:="effort" robot_controller:="effort_controller"
   ```
This will spawn the manipulator in gazebo and rviz. 
Then, open another terminal, connect to the same docker container and run:
   ```
   . install/setup.bash
   ros2 launch ros2_kdl_package kdl_node.launch.py
   ```
This will start a linear trajectory computed in the joint space with a polynomial velocity profile as default option.

 - In order to change velocity profile you can go in ros2_kdl_package/config/params.yaml 
and change the _vel_prof_ param from "cubic" to "trapezoidal".

 - In order to change the trajectory you need to change the _trajectory_ param from "linear" to "circular" in the same file 

 - Finally to switch from joint space control to operational space control you can change the _cmd_interface_ param from "effort_j" to "effort_o".

  Once you did all the desired changes you have to run:
   ```
   colcon build
   ```
And then again:
   ```
   . install/setup.bash
   ros2 launch iiwa_bringup iiwa.launch.py command_interface:="effort" robot_controller:="effort_controller"
   ```
Finally, in a different terminal, connected to the same docker container, you run:
   ```
   . install/setup.bash
   ros2 launch ros2_kdl_package kdl_node.launch.py
   ```