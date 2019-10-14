cmake_minimum_required(VERSION 3.5)
project(grid_map_core)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

## Find catkin macros and libraries
#find_package(catkin REQUIRED COMPONENTS)
find_package(ament_cmake REQUIRED)

## Define Eigen addons. 
include(cmake/${PROJECT_NAME}-extras.cmake)

## System dependencies are found with CMake's conventions
#find_package(Eigen3 REQUIRED)
# Solution to find Eigen3 with Saucy.
find_package(Eigen3 QUIET)
if(NOT EIGEN3_FOUND)
  find_package(PkgConfig REQUIRED)
  pkg_check_modules(EIGEN3 REQUIRED eigen3)
  set(EIGEN3_INCLUDE_DIR ${EIGEN3_INCLUDE_DIRS})
endif()

###########
## Build ##
###########

## Specify additional locations of header files
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIR}
)

## Declare a cpp library
add_library(${PROJECT_NAME}
   src/GridMap.cpp
   src/GridMapMath.cpp
   src/SubmapGeometry.cpp
   src/BufferRegion.cpp
   src/Polygon.cpp
   src/iterators/GridMapIterator.cpp
   src/iterators/SubmapIterator.cpp
   src/iterators/CircleIterator.cpp
   src/iterators/EllipseIterator.cpp
   src/iterators/SpiralIterator.cpp
   src/iterators/PolygonIterator.cpp
   src/iterators/LineIterator.cpp
   src/iterators/SlidingWindowIterator.cpp
)

#target_link_libraries(${PROJECT_NAME}
#  ${catkin_LIBRARIES}
#)

#############
## Install ##
#############

# Mark executables and/or libraries for installation
install(TARGETS ${PROJECT_NAME}
  DESTINATION lib/vision_info_server
)

# Mark cpp header files for installation
install(
  DIRECTORY "include/"
  DESTINATION include
)

# Mark other files for installation
install(DIRECTORY doc DESTINATION share/${PROJECT_NAME})

#############
## Testing ##
#############

#if(CATKIN_ENABLE_TESTING)
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
## Add gtest based cpp test target and link libraries
#catkin_add_gtest(${PROJECT_NAME}-test
#  test/test_grid_map_core.cpp
#  test/GridMapMathTest.cpp
#  test/GridMapTest.cpp
#  test/GridMapIteratorTest.cpp
#  test/LineIteratorTest.cpp
#  test/EllipseIteratorTest.cpp
#  test/SubmapIteratorTest.cpp
#  test/PolygonIteratorTest.cpp
#  test/PolygonTest.cpp
#  test/EigenPluginsTest.cpp
#  test/SpiralIteratorTest.cpp
#  test/SlidingWindowIteratorTest.cpp
#  )
#endif()

#if(TARGET ${PROJECT_NAME}-test)
#  target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
#endif()

ament_package()