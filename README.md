# ROS_edx

[Week1 - ROS Essentials](#week1)

[Week2 - Build your own robot environment](#week2)

## <a name="week1"> Week 1 - ROS Essentials</a>

#### Assignment 1

Implementing a node to be both a publisher and an subscriber.
##### 1. _Task 1_:
An ultrasound sensor is installed in a system. It is used for measuring the height of the boxes running on a conveyor belt. When there is no box, the sensor publishes the maximum range and when detecting one, it reports the distance to the top surface of the box. The  ***week1_assignment1.py*** is modified to achieve:
1. Subscribe to the /sensor_info topic.
2. Compute the height of the box from the sensor reading.
3. Filter out the false positives from the sensor due to sensor noise.

The result is located in the directory *src/hrwros/hwros_week1/scripts/week1_assignment1_task1.png*

##### 2. _Task 2_:
Create a new message type called BoxHeightInformation.msg containing the placeholder "box_height" which is a floating point number.
1. Create a new message type ***BoxHeightInformation.msg*** in the same folder where ***SensorInformation.msg*** file is located.

2. Add a place holder *box_height* of floating point number type in this message file.

3. Generate the new message type as instructed in the lecture. Then run

```
	rosmsg show hrwros_msgs/BoxHeightInformation
```

The screenshot of the result is located in the directory [src/hrwros/hwros_week1/scripts/week1_assignment1_task2.png](src/hrwros/hwros_week1/scripts/week1_assignment1_task2.png)

##### 3. _Task 3_:
Only publish a new topic "/box_height_info" when a valid box is detected.
1. Create an object of the new BoxHeightInformation message type when the detected box height is valid.
2. Create a publisher for the new massage type.
3. Publish the box height information on the */box_height_info* ONLY when the detected box has a valid height.

Start a new terminal:
```
	roscore
```
In a new terminal:
```
	rosrun hrwros_week1 week1_assignment1.py
```
In another terminal
```
	rostopic list
```
If the the topic */box_height_info* is listed, run:
```
	rostopic info /box_height_info
	rostopic echo /box_height_info
```

After 5 messages, terminate the execution.

The screenshot of the result is located in the directory gsrc/hrwros/hwros_week1/scripts/week1_assignment1_task3.png](src/hrwros/hwros_week1/scripts/week1_assignment1_task3.png)

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
