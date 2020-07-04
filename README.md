<img src="udacity_banner.jpg" height ="20">

### Robotics Software Engineer - Nanodegree

# Project 04 (of 05) : Map My World
## Directory Structure
```
.Map_My_World
   ├── my_robot
   │   ├── CMakeLists.txt
   │   ├── config
   │   │   ├── base_local_planner_params.yaml
   │   │   ├── costmap_common_params.yaml
   │   │   ├── global_costmap_params.yaml
   │   │   ├── local_costmap_params.yaml
   │   │   └── __MACOSX
   │   ├── launch
   │   │   ├── amcl.launch
   │   │   ├── config_rviz.rviz
   │   │   ├── localization.launch
   │   │   ├── mapping.launch
   │   │   ├── robot_description.launch
   │   │   ├── teleop.launch
   │   │   └── world.launch
   │   ├── maps
   │   │   ├── my_map.pgm  (!!upload this!!)
   │   │   └── my_map.yaml
   │   ├── meshes
   │   │   ├── hokuyo.dae
   │   │   └── RoboLeg.STL
   │   ├── package.xml
   │   ├── urdf
   │   │   ├── my_robot.gazebo
   │   │   └── my_robot.xacro
   │   └── worlds
   │       └── Avadhoot.world
   ├── teleop_twist_keyboard
   │   ├── CHANGELOG.rst
   │   ├── CMakeLists.txt
   │   ├── package.xml
   │   ├── README.md
   │   └── teleop_twist_keyboard.py
   ├── LICENSE
   ├── README.md
```  

## Project Goals
develop your own package to interface with the rtabmap_ros package.
addition of an RGB-D camera.
generate the appropriate launch files to launch the robot and map its surrounding environment.
When your robot is launched you will teleop around the room to collect the sensor data for generating the map.
Use the RTAB Mapping package to extract the map from the data collected.

## Output


## Environment
Tested on Ubuntu 16.04.6 LTS, ROS Kinetic, Boost 1.58

## Setup and run
Note: The commands in this README work, considering that the main workspace is located at ```/home/robond/workspace/catkin_ws/src```      
      Notice the ```robond``` username. Make appropriate changes for your system.
      
Warning: Some minor features will not work in your system if your username of the system is different.

[Click here for the fix and to learn more](#Missing-minor-feature)
#### 1. Update the Workspace image
```
$ sudo apt-get update && sudo apt-get upgrade -y 
```

#### 2. Clone the files in /home/workspace
```
$ cd /home/robond/workspace/catkin_ws/src
$ git clone https://github.com/Avadhoot94/Map_My_World.git
$ cd /home/robond/workspace/catkin_ws/src/Map_My_World
$ git clone https://github.com/ros-teleop/teleop_twist_keyboard
```
#### 3. Build the package
```
$ cd /home/robond/workspace/catkin_ws
$ catkin_make
$ source devel/setup.bash
````
#### 4. Launch the world and the robot
```
$ roslaunch my_robot world.launch
```
Make sure the ```fixed frame``` in ```RViz``` is ```odom```

#### 5. Launch the mapping node
**Remember, relaunching the mapping node deletes any previously mapped database in place on launch start up!**
```
$ roslaunch my_robot mapping.launch
```
#### 6. Launch the teleop node
```
$ roslaunch my_robot teleop.launch
```
#### 7. Collect environment data
Drive around in the world using the keyboard controls from ```teleop``` node.
The RGB-D camera on the robot will collect the data for generating the map.
For best results, go over similar paths two or three times.

Once data collection is done, stop the mapping node by pressing ```Ctrl```+``` C```
The data will be stored as ```rtabmap.db``` in the following file location:

```/home/robond/workspace/catkin_ws/src/Map_My_World/my_robot/maps```

**Remember, relaunching the mapping node deletes any previously mapped database in place on launch start up!**

#### 8. Explore the generated map using ```rtabmap-databaseViewer```
```
$ rtabmap-databaseViewer /home/robond/workspace/catkin_ws/src/Map_My_World/my_robot/maps/rtabmap.db
```



## Missing minor feature
The ```~/Where_Am_I/my_robot/world/Avadhoot.world``` file uses ```~/Where_Am_I/my_robot/meshes/RoboLeg.STL``` for the legs of the **static** robot model as indicated in the picture below:

<img src="output/Reference_roboleg.PNG" width="500" >

<p>&nbsp;</p>

The ```Avadhoot.world``` file thus, contains the directory address of the ```RoboLeg.STL``` as ```/home/robond/workspace/catkin_ws/src/Where_Am_I/my_robot/meshes/RoboLeg.STL```<br/> **Replace all** the addresses appropriately to see the legs. 

Else the package will **run without errors** but without the legs as seen below:

<img src="output/Reference_roboleg_error.PNG" width="500" >
