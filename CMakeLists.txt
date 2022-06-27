cmake_minimum_required(VERSION 2.8.3)
project(assistive_cane)

find_package(catkin REQUIRED COMPONENTS
  rospy
  roscpp
  std_msgs
  geometry_msgs
  sensor_msgs
  visualization_msgs
  message_generation
)

catkin_python_setup()

add_message_files(
  FILES
  cane_command_msg.msg
)

generate_messages(
   DEPENDENCIES
   std_msgs
)

catkin_package(CATKIN_DEPENDS message_runtime)