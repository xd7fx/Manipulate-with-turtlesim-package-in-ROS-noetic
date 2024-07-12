# TurtleSim on ROS

This repository provides a guide to install and run the TurtleSim package on ROS (Robot Operating System). It also includes instructions for exploring topics, nodes, and services, and controlling the turtle using keyboard commands.

## Prerequisites

- Ubuntu (20.04 or later)
- ROS Noetic installed

## Installation

1. Update your package list:
    ```bash
    sudo apt-get update
    ```

2. Install the TurtleSim package:
    ```bash
    sudo apt-get install ros-$(rosversion -d)-turtlesim
    ```
![لقطة الشاشة 2024-07-11 194638](https://github.com/user-attachments/assets/b2d28b9c-7f1e-4970-9e3d-c0f72653dd7b)

## Running TurtleSim

1. Launch the ROS core:
    ```bash
    roscore
    ```

2. In a new terminal, run the TurtleSim node:
    ```bash
    rosrun turtlesim turtlesim_node
    ```
![لقطة الشاشة 2024-07-11 194638](https://github.com/user-attachments/assets/dac8e225-99cf-426c-8a2b-30c1257b668e)

3. A new window should open displaying the TurtleSim environment with a turtle in the center.

## Exploring Nodes and Topics

### List Active Nodes

To list all active nodes:
  ```bash
  rosnode list
  ```
![لقطة الشاشة 2024-07-11 222706](https://github.com/user-attachments/assets/c9ecf4ff-0865-48f1-b4d3-96dd3d334602)


### Get Node Information

To get detailed information about a specific node (e.g., `/turtlesim`):
  ```bash
  rosnode info /turtlesim
  ```
1. Publications:
   
**`/rosout [rosgraph_msgs/Log]`**: This node publishes ROS system log messages to the /rosout topic. These messages can be used for system tracking and diagnostics.

**`/turtle1/color_sensor [turtlesim/Color]`**: This node publishes turtle color sensor data to the /turtle1/color_sensor topic.

**`/turtle1/pose [turtlesim/Pose]`**: This node publishes the turtle's pose (coordinates and angle) to the /turtle1/pose topic.

2. Subscriptions:

**`/turtle1/cmd_vel [unknown type]`**: This node subscribes to the /turtle1/cmd_vel topic to receive velocity commands and move the turtle accordingly. The message type is unknown here but is typically geometry_msgs/Twist.

3. Services:

**`/clear`**: Service to clear the screen.

**`/kill`**: Service to kill a specified turtle.

**`/reset`**: Service to reset the simulation.

**`/spawn`**: Service to spawn a new turtle at a specified location.

**`/turtle1/set_pen`**: Service to set the turtle's pen color, line width, and whether to raise or lower the pen.

**`/turtle1/teleport_absolute`**: Service to teleport the turtle to an absolute position.

**`/turtle1/teleport_relative`**: Service to teleport the turtle relative to its current position.

**`/turtlesim/get_loggers`**: Service to get information about the system's loggers.

**`/turtlesim/set_logger_level`**: Service to set the logging level of the system.

![لقطة الشاشة 2024-07-11 222706](https://github.com/user-attachments/assets/45e1a825-5dce-4c21-b177-dd733f0d4f0b)


### List Active Topics

To list all active topics:
  ```bash
  rostopic list
  ```
**`/rosout`**: For logging messages in the ROS system.

**`/rosout_agg`**: For aggregating and displaying logged messages. 

**`/turtle1/cmd_vel`**: For sending movement (velocity) commands to the turtle.

**`/turtle1/color_sensor`**: For publishing color sensor data from the turtle.

**`/turtle1/pose`**: For publishing the turtle's pose (coordinates and orientation).

![لقطة الشاشة 2024-07-11 223528](https://github.com/user-attachments/assets/6597ca7a-ab95-4a21-89a9-45f58904cfcc)


### Get Topic Information

To get detailed information about a specific topic (e.g., `/turtle1/pose`):
  ```bash
  rostopic info /turtle1/pose
  ```
This command provides information about the turtle1/pose topic. The results include:

Type: The type of data being sent on the topic, which is turtlesim/Pose.

Publishers: Nodes publishing to this topic, which are:

/turtlesim

Subscribers: There are no subscribers to this topic.

![لقطة الشاشة 2024-07-11 223929](https://github.com/user-attachments/assets/1f4c08b0-bc65-460a-a91b-22426a9c7953)
### Displaying the Type of the turtle1/pose Topic
  ```bash
  rostopic type /turtle1/pose
  ```
This command shows the type of data being sent on the topic, which is turtlesim/Pose.

![لقطة الشاشة 2024-07-11 223929](https://github.com/user-attachments/assets/29b78866-1413-40ad-8ecb-088de3360822)


### Show Message Structure

To display the message structure for a specific topic type (e.g., `turtlesim/Pose`):
  ```bash
  rosmsg show turtlesim/Pose
  ```
This command displays the message structure of turtlesim/Pose. The results include:

float32 x

float32 y

float32 theta

float32 linear_velocity

float32 angular_velocity

![لقطة الشاشة 2024-07-11 224213](https://github.com/user-attachments/assets/9c4fb883-189a-4a64-bf7b-a9628c834ff5)
### Reading Data from the turtle1/pose Topic
  ```bash
  rostopic echo /turtle1/pose
  ```
This command displays the data being sent on the turtle1/pose topic. The results show the turtle's coordinates and velocity values as follows:

![لقطة الشاشة 2024-07-11 224813](https://github.com/user-attachments/assets/3bc2cca4-9dcf-458d-868d-41bc2911bfc8)
### Displaying the Type of the turtle1/cmd_vel Topic:
  ```bash
  rostopic type /turtle1/cmd_vel
  ```
This command shows the type of data being sent on the topic, which is geometry_msgs/Twist.

![لقطة الشاشة 2024-07-11 225144](https://github.com/user-attachments/assets/749e5b65-fa65-4408-a983-d09a0aa2f763)

### Publishing a Message to the turtle1/cmd_vel Topic:
  ```bash
  rostopic pub -1 /turtle1/cmd_vel geometry_msgs/Twist '{linear: {x: 1.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.0}}'
  ```
This command publishes a single message (using the -1 option) to the turtle1/cmd_vel topic with specified linear and angular values to move the turtle in a circular pattern.

![لقطة الشاشة 2024-07-11 230136](https://github.com/user-attachments/assets/53975c79-fb08-4d5a-9bd9-6406d023d238)


### Resetting the Turtle:
In the terminal on the left, the command:
  ```bash
  rosservice call /reset
  ```
was used to call the reset service for the turtle, returning it to its original position in the TurtleSim window.

![لقطة الشاشة 2024-07-11 230634](https://github.com/user-attachments/assets/5638007d-6800-445e-b154-0815d2acd934)
### Publishing a New Message to Move the Turtle:
After resetting, the following command was used to publish a message to move the turtle:
  ```bash
  rostopic pub /turtle1/cmd_vel geometry_msgs/Twist -r 1 -- '[2.0,0.0,0.0]' '[0.0,0.0,1.8]'
  ```
This command publishes a repeated message (at 1 Hz) to the turtle1/cmd_vel topic with specified linear and angular values to move the turtle in a wider circular pattern.

![لقطة الشاشة 2024-07-11 230634](https://github.com/user-attachments/assets/83a7df20-e55c-444f-8255-4ded24de85bb)
![لقطة الشاشة 2024-07-11 230850](https://github.com/user-attachments/assets/51610bf2-4d28-4701-a3cf-74534b5ba682)
![لقطة الشاشة 2024-07-11 231025](https://github.com/user-attachments/assets/1c59c7b1-f475-49ed-b030-6bcd3ce047b2)


### Checking the Publish Rate of the turtle1/cmd_vel Topic:
  ```bash
  rostopic hz /turtle1/cmd_vel
  ```
This command shows the publish rate of the turtle1/cmd_vel topic. The results show that the rate is 1.0 Hz, meaning messages are published at a rate of one message per second.

![لقطة الشاشة 2024-07-11 231447](https://github.com/user-attachments/assets/a2f4a563-8a92-4dd2-8b5b-f1b22c4ebdfd)
### Checking the Publish Rate of the turtle1/pose Topic:
  ```bash
  rostopic hz /turtle1/pose
  ```
This command shows the publish rate of the turtle1/pose topic. The results show that the rate is approximately 62.5 Hz, meaning messages are published at a rate of 62.5 messages per second. The results include:

![لقطة الشاشة 2024-07-11 231551](https://github.com/user-attachments/assets/4d218c9a-371c-45b0-a6af-41bb4edc0df1)

### Running rqt_graph:
  ```bash
  rosrun rqt_graph rqt_graph
  ```
This command uses rosrun to run the rqt_graph tool, which displays a graph of the nodes and topics in ROS.
Node Graph:

The window that appears below the terminal on the left shows the node graph. The results include:

The node /rostopic_39298_1720728734153 publishes to the topic /turtle1/cmd_vel.

The topic /turtle1/cmd_vel connects to the node /turtlesim.

![لقطة الشاشة 2024-07-11 231702](https://github.com/user-attachments/assets/8ef8a2fa-c982-4adb-b303-45c3e62273df)


## Controlling the Turtle

### Using Keyboard

1. In a new terminal, run the teleop node to control the turtle using the keyboard:
    ```bash
    rosrun turtlesim turtle_teleop_key
    ```

2. Use the arrow keys to move the turtle. Press `q` to quit.

![لقطة الشاشة 2024-07-11 232435](https://github.com/user-attachments/assets/0aaf934d-6dfd-4b7b-9773-07531f3e79b2)
![لقطة الشاشة 2024-07-11 232521](https://github.com/user-attachments/assets/930248f4-f35b-4f44-9372-8704f0e25b73)

### Listing ROS Nodes:
  ```bash
  rosnode list
  ```
### Getting Information About the teleop_turtle Node:
  ```bash
  rosnode info /teleop_turtle
  ```
was used to get detailed information about the /teleop_turtle node. The results include:

![لقطة الشاشة 2024-07-11 232702](https://github.com/user-attachments/assets/c238e02b-5b50-4fa5-a31f-4dfb87e89039)
### Getting Information About the turtle1/cmd_vel Topic:
  ```bash
  rostopic info /turtle1/cmd_vel
  ```
This command provides information about the turtle1/cmd_vel topic. The results include:

![لقطة الشاشة 2024-07-11 232845](https://github.com/user-attachments/assets/518c30c6-9790-4465-b3d1-8f97bd93f552)
![لقطة الشاشة 2024-07-11 233044](https://github.com/user-attachments/assets/b64f96a3-71bb-4b92-9aba-937f911d6bf4)
![لقطة الشاشة 2024-07-11 233217](https://github.com/user-attachments/assets/410b11ff-2ae1-4332-8c1f-5045d25d0ae9)
![لقطة الشاشة 2024-07-11 233319](https://github.com/user-attachments/assets/0a1794e8-4121-4537-82f1-b01337c18ab0)
![لقطة الشاشة 2024-07-11 233953](https://github.com/user-attachments/assets/dddbbae8-1cd0-4d10-9ec8-8430c026aedd)

### Getting Help for rostopic Commands

To display help for `rostopic` commands:
  ```bash
  rostopic --help
  ```
![لقطة الشاشة 2024-07-11 233439](https://github.com/user-attachments/assets/95c1e751-4c4a-41c2-a092-46b2fb58997c)

