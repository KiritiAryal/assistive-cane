# assistive-cane
## Release code for SoNIC 2022

### This is the project I did with SONIC lab at Cornell. We made a smart assistive cane for visually impaired. It was successfully able to prevent bumping into obstacles in a controlled environment.
Below is the link for a short youtube video presentation of the whole program from Cornell.

[Sonic Program](https://www.youtube.com/watch?v=j8Jo-ZJdJWY)



For future me, to understand how we went through to accomplish our goal:

ROS Nodes and Communication:

Nodes:
smart_cane.py: Primary script representing the smart cane behavior and control logic. It's a ROS node that subscribes to the /cane_state topic for the current pose of the cane and publishes vibration commands to the /cane_command topic.
run_cane.py: A script representing the physical execution of the smart cane. It subscribes to the /cane_command topic to receive vibration commands and controls the cane's actuators accordingly.
Communication:
cane_command_msg.msg: Defines the message structure for vibration commands, facilitating communication between smart_cane.py and run_cane.py.
Path Planning and A Algorithm:*

assistive_cane/astar.py: Contains the implementation of the A* algorithm for path planning. Used by smart_cane.py to generate a path from the current cane position to a goal position, considering obstacles.
assistive_cane/world_visualizer.py: Provides visualization tools for visualizing the world, including cane and box positions.
Hardware Interface and Ultrasonic Sensing:

run_cane.py interacts with the physical hardware, including actuators for vibration (forward, left, right) and an ultrasonic sensor represented by the Ultrasonic class. The Ultrasonic class is responsible for updating the distance attribute based on sensor readings.
Launch Files and System Configuration:

perception.launch: Configures a static transform between the "map" and "camera_link" frames. This is vital for providing spatial context to perception data.
ROS Workspace Setup:

ros_buster.sh: A script for setting up a ROS Catkin workspace, installing dependencies, and building ROS packages. Ensures the installation of ROS Noetic on a system running Debian Buster.
Visualization:

visualize_world.rviz: Configuration file for RViz, a visualization tool for ROS. It defines various visualization elements, including grids, images, point clouds, and marker arrays.
Execution Flow:
Initialization:

ros_buster.sh initializes the ROS environment on the target system with ROS Noetic.
perception.launch sets up a static transform between the "map" and "camera_link" frames.
Smart Cane Path Planning:

smart_cane.py initializes a ROS node, subscribes to the /cane_state topic, and waits for the current cane pose and box positions.
It uses the A* algorithm (assistive_cane/astar.py) to generate a path from the current cane position to a specified goal, considering obstacle positions.
Execution:

run_cane.py initializes a ROS node, subscribes to the /cane_command topic, and interacts with the physical hardware.
It uses an ultrasonic sensor to measure distances in front of the cane (Ultrasonic class).
Vibration commands are received from smart_cane.py, and actuators are controlled accordingly.
Visualization:

RViz (visualize_world.rviz) is used to visualize the world, including cane and box positions, point clouds, and marker arrays.
Achievements:
The system aims to achieve an assistive smart cane capable of path planning and execution. Key components include:

Path Planning: Utilizes the A* algorithm for generating collision-free paths from the current cane position to a specified goal.
Execution: run_cane.py receives vibration commands from the smart cane script (smart_cane.py) and controls the cane's actuators accordingly.
Visualization: RViz is employed to visualize the world, providing insights into the cane's position, the environment, and the execution of the planned path.
The system is structured to leverage ROS for modular and scalable development, with separate scripts handling perception, control, and hardware interaction. The visualization tools enhance the debugging and monitoring process.
