cmake_minimum_required(VERSION 3.5)
project(grid_map_msgs)

find_package(ament_cmake REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)

#######################################
## Declare ROS messages and services ##
#######################################

## Generate messages in the 'msg' folder
set(msg_files
  "msg/GridMapInfo.msg"
  "msg/GridMap.msg"
)

## Generate services in the 'srv' folder
set(srv_files
  "srv/SetGridMap.srv"
  "srv/GetGridMap.srv"
  "srv/GetGridMapInfo.srv"
  "srv/ProcessFile.srv"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
  DEPENDENCIES std_msgs geometry_msgs
  ADD_LINTER_TESTS
)

ament_export_dependencies(rosidl_default_runtime)
ament_package()