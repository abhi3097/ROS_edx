# ROS_edx

[Week1 - ROS Essentials](#week1)

[Week2 - Build your own robot environment](#week2)

[Week3 - Autonomous navigation](#week3)

[Week4 - Manipulation](#week4)

[Week5 - Robot vision](#week5)


## <a name="week1"> Week 1 - ROS Essentials</a>

#### Assignment 1
Implementing a node to be both a publisher and an subscriber.
##### 1. _Task 1_:
An ultrasound sensor is installed in a system. It is used for measuring the height of the boxes running on a conveyor belt. When there is no box, the sensor publishes the maximum range and when detecting one, it reports the distance to the top surface of the box. The  ***week1_assignment1.py*** is modified to achieve:
1. Subscribe to the /sensor_info topic.
2. Compute the height of the box from the sensor reading.
3. Filter out the false positives from the sensor due to sensor noise.

The result is located in the directory [src/hrwros/hrwros_week1/scripts/week1_assignment1_task1.png](src/hrwros/hrwros_week1/scripts/week1_assignment1_task1.png)

##### 2. _Task 2_:
Create a new message type called BoxHeightInformation.msg containing the placeholder "box_height" which is a floating point number.
1. Create a new message type ***BoxHeightInformation.msg*** in the same folder where ***SensorInformation.msg*** file is located.

2. Add a place holder *box_height* of floating point number type in this message file.

3. Generate the new message type as instructed in the lecture. Then run

```
$ $ rosmsg show hrwros_msgs/BoxHeightInformation
```

The screenshot of the result is located in the directory [src/hrwros/hrwros_week1/scripts/week1_assignment1_task2.png](src/hrwros/hrwros_week1/scripts/week1_assignment1_task2.png)

##### 3. _Task 3_:
Only publish a new topic "/box_height_info" when a valid box is detected.
1. Create an object of the new BoxHeightInformation message type when the detected box height is valid.
2. Create a publisher for the new massage type.
3. Publish the box height information on the */box_height_info* ONLY when the detected box has a valid height.

Start a new terminal:
```
$ roscore
```
In a new terminal:
```
$ rosrun hrwros_week1 week1_assignment1.py
```
In another terminal
```
$ rostopic list
```
If the the topic */box_height_info* is listed, run:
```
$ rostopic info /box_height_info
$ rostopic echo /box_height_info
```

After 5 messages, terminate the execution.

The screenshot of the result is located in the directory [src/hrwros/hrwros_week1/scripts/week1_assignment1_task3.png](src/hrwros/hrwros_week1/scripts/week1_assignment1_task3.png)


## <a name="week2"> Week 2 - Build your own robot environment </a>
#### Assignment 1
Add an extra bin opposite to the robot.
Correct implementations will show:
1. an extra bin in the factory
2. the bin must be on the floor, not in the floor or slightly above it
3. located opposite Robot 1 (ie: on the other side of the conveyor, as indicated by the red arrows in the two illustrations above)
4. not touching anything other than the floor
The screenshot of the result is located in the directory [src/hrwros_week2/urdf/hrwros_week2_assignment1.png](src/hrwros_week2/urdf/hrwros_week2_assignment1.png)

#### Assignment 2
Add a sphere under the staircase. Correct implementations will show:

1. a new, green sphere in the factory
2. radius: 40 centimeters
3. the sphere must be on the floor, not in the floor or slightly above it
4. located under the stairs (as indicated by the red arrows in the two illustrations above)
5. not touching anything other than the floor
The screenshot of the result is located in the directory [src/hrwros_week2/urdf/hrwros_week2_assignment2.png](src/hrwros_week2/urdf/hrwros_week2_assignment2.png)

#### Assignment 3
Replace the robot ur5 with a provided robot. Correct implementations will show:
Correct implementations will show:

1. the new robot model properly mounted on the pedestal where Robot 2 is now
2. the new robot with an identical orientation (ie: rotation) as Robot 2: in its startup pose, the replacement robot 3. should point in the same direction as the UR5. The replacement robot does not need to completely mimic the position of all joints and links of the UR5.
4. the robot must be on the pedestal, not in the pedestal or slightly above it
5. not touching anything other than the pedestal
The screenshot of the result is located in the directory [src/hrwros_week2/urdf/hrwros_week2_assignment3.png](src/hrwros_week2/urdf/hrwros_week2_assignment3.png)


## <a name="week3"> Week 3 - Autonomous navigation </a>
#### Assignment 1
##### 1. _Task 1_:
In this first part we will prepare for navigation in our factory world.

1. Launch the hrwros factory simulation with:
```
$ roslaunch hrwros_gazebo hrwros_environment.launch
```

***Note***: If you are not successful in launching the environment, retry.

2. Launch AMCL with a map of the factory we created:
```
$ roslaunch turtlebot_gazebo amcl_demo.launch map_file:=$HOME/hrwros_ws/src/hrwros_week3/config/map_factory_v1.yaml
```
3. Next, start the RViz navigation visualization:
```
$ roslaunch turtlebot_rviz_launchers view_navigation.launch
```
Change *robot_description* to *turtlebot_description* under *RobotModel*.
The screenshot of the result is located in the directory [src/hrwros_week3/week3_assignment1_task1.png](src/hrwros_week3/week3_assignment1_task1.png)

##### 2. _Task 2_:
Find the location of the robot under *Model* -> *mobile_base* of Gazebo and run:
```
$ roslaunch turtlebot_gazebo amcl_demo.launch map_file:=$HOME/hrwros_ws/src/hrwros_week3/config/map_factory_v1.yaml initial_pose_x:=<XCOORD> initial_pose_y:=<YCOORD>
```
The screenshot of the result is located in the directory [src/hrwros_week3/week3_assignment1_task2.png](src/hrwros_week3/week3_assignment1_task2.png)

##### 3. _Task 3_:
Navigating the turtlebot around the factory.
```
$ roslaunch turtlebot_teleop keyboard_teleop.launch
```
The screenshot of the result is located in the directory [src/hrwros_week3/week3_assignment1_task3.png](src/hrwros_week3/week3_assignment1_task3.png)

***Note***: Keep the terminal with teleop active while navigating.

#### Assignment 2 - Pathing
##### 1. _Task 1_: Visualize the planning
In Rviz *Add* -> *Path* -> *Topic* -> */move_base/NavfnROS/plan*

The screenshot of the result is located in the directory [src/hrwros_week3/week3_assignment2_task1.png](src/hrwros_week3/week3_assignment2_task1.png)

##### 2. _Task 2_: Visualize the planning

1. Add a new path display and subscribe it to */move_base/DWAPlannerROS/global_plan*. Change the colour from green to blue (0; 0; 255).

2. Do the same for */move_base/DWAPlannerROS/local_plan*, and colour  it red (255; 0; 0).

The screenshot of the result is located in the directory [src/hrwros_week3/week3_assignment2_task2.png](src/hrwros_week3/week3_assignment2_task2.png)

#### Assignment 3 - Navigating using a ROS Node
##### 1. _Task 1_:
Update the position of the 1st target of the turtlebot in the file ***week3_assignment3_part1.py*** using the information under *TF* ->*turtlebot_target1*.
Run:
```
$ roslaunch hrwros_gazebo hrwros_environment.launch
$ roslaunch turtlebot_gazebo amcl_demo.launch map_file:=$HOME/hrwros_ws/src/hrwros_week3/config/map_factory_v1.yaml initial_pose_x:=<A> initial_pose_y:=<B>
$ roslaunch turtlebot_rviz_launchers view_navigation.launch
$ roslaunch hrwros_week3 week3_assignment3_part1.launch
```
The screenshot of the result is located in the directory [src/hrwros_week3/week3_assignment3_task1.jpg](src/hrwros_week3/week3_assignment3_task1.jpg)

##### 2. _Task 2_:
The first goal is to navigate the TurtleBot to its second target location, following similar steps as you followed in the first part. In the second part, the goal is to visualize and become aware of the ***"unknown obstacle avoidance"***. Update the position of the 1st target of the turtlebot in the file ***week3_assignment3_part2.py*** using the information under *TF* ->*turtlebot_target2*.
```
$ roslaunch hrwros_week3 week3_assignment3_part2.launch
```
The screenshot of the result is located in the directory [src/hrwros_week3/week3_assignment3_task2.jpg](src/hrwros_week3/week3_assignment3_task2.jpg)


## <a name="week4"> Week 4 - Manipulation</a>

#### Assignment 1 Modifying an existing MoveIt! configuration package

Add six new Robot Poses

```
$ roslaunch week4_moveit_config setup_assistant.launch
```

The screenshot of the result is located in the directory [src/hrwros_week4/week4_assignment1.png](src/hrwros_week4/week4_assignment1.png)

#### Assignment 2 Write a moveit commander script

1. Open a new terminal and source the workspace setup files. Start the factory simulation with:
```
$ roslaunch hrwros_gazebo hrwros_environment.launch
```

2. Outside the terminal, in your favorite editor, create a new file called ***week4_assignment2_script*** in ***$HOME/hrwros_ws/src/hrwros_week4/scripts*** folder.

3. Add a sequence of moveit commander scripts such that robot2 executes the following motions:

  1. First the robot2 goes to the R2Up configuration

  2. Then robot2 goes to the R2Home configuration.

  3. Then robot2 goes to the R2PreGrasp configuration.

  4. Then the end effector of robot2 moves linearly down by 25cm.

4. Then, start MoveIt! commander with the following command in the same file path where you created your script, that is:

```
$ roscd hrwros_week4/scripts

$ rosrun hrwros_week4 hrwros_moveit_commander_cmdline
```

5. And then you can run your script on the MoveIt! commander prompt that shows up

The screenshot of the result is located in the directory [src/hrwros_week4/week4_assignment2.jpg](src/hrwros_week4/week4_assignment2.jpg)

#### Assignment 3
Using the MoveGroup Interface for implementing a simple pick and place pipeline for robot2 on the same lines as we did for robot1
1. Complete the script ***week4_assignment3.py*** in the hrwros_week4 package wherever you are instructed with *write your code here*.

2. After you have completed the script, start the factory simulation in a new terminal with:
```
$ roslaunch hrwros_gazebo hrwros_environment.launch
```

3. Then, make sure to adjust the perspective of the Gazebo Simulation to have a clear view of Robot2.

4. In another terminal, first navigate to the ***hrwros_week4/scripts*** folder with roscd. Make the ***week4_assignment3.py*** script executable.

5. Finally, run the command:

```
$ roslaunch hrwros_week4 week4_assignment3.launch
```

The screenshot of the result is located in the directory [src/hrwros_week4/week4_assignment3.jpg](src/hrwros_week4/week4_assignment3.jpg)


## <a name="week5"> Week 5 - Robot vision</a>

#### Assignment 1 Install and configure logical cameras
##### 1. _Task 1_: Install cameras
Add the logical camera to the world.
* Camera 1: 1.2  1.8  2.0 0 1.57 0
* Camera 2:-8.3 -1.23 1.8 0 1.57 0

The screenshot of the result is located in the directory [src/hrwros_week5/week5_assignment1_task1.png](src/hrwros_week5/week5_assignment1_task1.png)

##### 2. _Task 2_: Configure cameras
Configure the logical cameras accordingly.

***Configuration for Logical Camera 1:***
* Model name: logical_camera_1
* Link name: logical_camera_1_link
* Sensor name: logical_camera_1

***Configuration for Logical Camera 2:***
* Model name: logical_camera_2
* Link name: logical_camera_2_link
* Sensor name: logical_camera_2

```
$ roslaunch hrwros_gazebo hrwros_environment.launch
```

The screenshot of the result is located in the directory [src/hrwros_week5/week5_assignment1_task2.hpg](src/hrwros_week5/week5_assignment1_task2.jpg)

#### Assignment 2 TF command line tools
##### 1. _Task 1_: View_frames and tf_echo:

1. Start the factory simulation with: ```roslaunch hrwros_gazebo hrwros_environment.launch```

2. In a new terminal, execute the command: ```rosrun tf view_frames```

3. Then, open the ***frames.pdf*** file. Verify that the TF frames ***logical_camera_1_frame*** and ***logical_camera_2_frame*** are now a part of the TF tree and and the entire TF tree is connected without any breaks.

4. Now, go back to the terminal where you executed the view_frames command and execute the command ```rosrun tf tf_echo logical_camera_2_frame camera_rgb_frame```

The screenshot of the result is located in the directory [src/hrwros_week5/week5_assignment2_task1.png](src/hrwros_week5/week5_assignment2_task1.png)

##### 2. _Task 2_: Static_transform_publisher and RViz Visualization
Use the static_transform_publisher to publish a static transform between the plate_top_link and a new frame called turtlebot_object_top which will be located 20cm on top of the TurtleBot.

1. Start the simulation in RViz as
``` $ roslaunch hrwros_gazebo hrwros_environment.launch```

2. Then add an additional Robot Model display and modify the ***robot_description*** to ***turtlebot_description***.
3. Now, enable the TF visualization such that only the ***plate_top_link*** frame is shown.

4. Start a new terminal. Publish a static transform between ***plate_top_link*** and a new frame ***turtlebot_object_top*** such that the ***turtlebot_object_top frame*** is 20cm above ***plate_top_link***. Recall that a static transform can be published as follows:
```
$ rosrun tf2_ros static_transform_publisher <specify_correct_translation> 0 0 0 1 plate_top_link turtlebot_object_top
```

5. Go back to RViz and enable the newly published frame turtlebot_object_top. It should show up exactly on top of the reference frame for plate_top_link.

6. Now in a new terminal, start the turtlebot teleoperation with:
```
$ roslaunch turtlebot_teleop keyboard_teleop.launch
```

Move the TurtleBot around with the keyboard to a different location of your choice and notice that the newly published TF frame ***turtlebot_object_top*** moves along with the TurtleBot.

The screenshot of the result is located in the directory [src/hrwros_week5/week5_assignment2_task2.png](src/hrwros_week5/week5_assignment2_task2.png)

#### Assignment 3
Using the MoveGroup Interface for implementing a simple pick and place pipeline for robot2 on the same lines as we did for robot1
1. Complete the script ***week4_assignment3.py*** in the hrwros_week4 package wherever you are instructed with *write your code here*.

2. After you have completed the script, start the factory simulation in a new terminal with:
```
roslaunch hrwros_gazebo hrwros_environment.launch.
```

3. Then, make sure to adjust the perspective of the Gazebo Simulation to have a clear view of Robot2.

4. In another terminal, first navigate to the ***hrwros_week4/scripts*** folder with roscd. Make the ***week4_assignment3.py*** script executable.

5. Finally, run the command:
```
roslaunch hrwros_week4 week4_assignment3.launch
```

The screenshot of the result is located in the directory [src/hrwros/hrwros_week1/scripts/week4_assignment3.jpg](src/hrwros/hrwros_week1/scripts/week1_assignment3.jpg)
