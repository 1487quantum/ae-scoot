cmake_minimum_required(VERSION 2.8.3)
project(drive_controller)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS nodelet roscpp trajectory_msgs geometry_msgs sensor_msgs nav_msgs tf)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

#######################################
## Declare ROS messages and services ##
#######################################

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   geometry_msgs#   trajectory_msgs
# )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
  INCLUDE_DIRS include
  LIBRARIES base_controller base_controller_nodelet
	base_twist base_twist_nodelet
	base_pose base_pose_nodelet
	basic_twist_integrator basic_twist_integrator_nodelet
  CATKIN_DEPENDS geometry_msgs nodelet roscpp trajectory_msgs
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

## Declare a cpp library
add_library(base_controller
  src/base_controller.cpp
)
add_library(base_controller_nodelet
  src/base_controller_nodelet.cpp
)
add_library(base_pose
  src/base_pose.cpp
)
add_library(base_pose_nodelet
  src/base_pose_nodelet.cpp
)
add_library(base_twist
  src/base_twist.cpp
)
add_library(base_twist_nodelet
  src/base_twist_nodelet.cpp
)
add_library(basic_twist_integrator
  src/basic_twist_integrator.cpp
)
add_library(basic_twist_integrator_nodelet
  src/basic_twist_integrator_nodelet.cpp
)

## Declare a cpp executable
add_executable(base_controller_node src/base_controller_node.cpp)
add_executable(base_pose_node src/base_pose_node.cpp)
add_executable(base_twist_node src/base_twist_node.cpp)
add_executable(basic_twist_integrator_node src/basic_twist_integrator_node.cpp)

## Add cmake target dependencies of the executable/library
## as an example, message headers may need to be generated before nodes
# add_dependencies(base_controller_node base_controller_generate_messages_cpp)

## Specify libraries to link a library or executable target against
target_link_libraries(base_controller
  ${catkin_LIBRARIES}
)
target_link_libraries(base_controller_nodelet
  ${catkin_LIBRARIES}
  base_controller
)
target_link_libraries(base_controller_node
  ${catkin_LIBRARIES}
  base_controller
)
target_link_libraries(base_pose
  ${catkin_LIBRARIES}
)
target_link_libraries(base_pose_nodelet
  ${catkin_LIBRARIES}
  base_pose
)
target_link_libraries(base_pose_node
  ${catkin_LIBRARIES}
  base_pose
)
target_link_libraries(base_twist
  ${catkin_LIBRARIES}
)
target_link_libraries(base_twist_nodelet
  ${catkin_LIBRARIES}
  base_twist
)
target_link_libraries(base_twist_node
  ${catkin_LIBRARIES}
  base_twist
)
target_link_libraries(basic_twist_integrator
  ${catkin_LIBRARIES}
)
target_link_libraries(basic_twist_integrator_nodelet
  ${catkin_LIBRARIES}
  basic_twist_integrator
)
target_link_libraries(basic_twist_integrator_node
  ${catkin_LIBRARIES}
  basic_twist_integrator
)

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
install(TARGETS base_controller base_controller_nodelet base_controller_node
	base_pose base_pose_nodelet base_pose_node
	base_twist base_twist_nodelet base_twist_node
	basic_twist_integrator basic_twist_integrator_nodelet basic_twist_integrator_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

## Mark cpp header files for installation
install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"
  PATTERN ".svn" EXCLUDE
)

## Mark other files for installation (e.g. launch and bag files, etc.)
install(FILES
  nodelet_plugins.xml
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_base_controller.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
