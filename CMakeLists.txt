cmake_minimum_required(VERSION 2.8.3)
project(uwvs_osl)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  image_transport
  roscpp
  sensor_msgs
  std_msgs
  OpenCV REQUIRED
  VISP REQUIRED
  message_generation
)
add_message_files(
  FILES
  PilotRequest.msg
)
generate_messages(
  DEPENDENCIES
  std_msgs
)
catkin_package(
	DEPENDS
	VISP
	CATKIN_DEPENDS message_runtime
)
## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)
include_directories(
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
  ${VISP_INCLUDE_DIRS}
)
message(STATUS ${OpenCV_INCLUDE_DIRS} ${VISP_INCLUDE_DIRS})

add_executable( robot_color_simple src/robot_cntrl_color_simple.cpp )
target_link_libraries ( robot_color_simple ${OpenCV_LIBRARIES} ${catkin_LIBRARIES} ${VISP_LIBRARIES})

add_executable( robot_uwsim src/robot_cntrl_uwsim.cpp )
target_link_libraries ( robot_uwsim ${OpenCV_LIBRARIES} ${catkin_LIBRARIES} ${VISP_LIBRARIES})

add_executable( robot_nessie src/robot_cntrl_nessie.cpp )
target_link_libraries ( robot_nessie ${OpenCV_LIBRARIES} ${catkin_LIBRARIES} ${VISP_LIBRARIES})

add_executable( robot_nessie_front src/robot_cntrl_nessie_front.cpp )
target_link_libraries ( robot_nessie_front ${OpenCV_LIBRARIES} ${catkin_LIBRARIES} ${VISP_LIBRARIES})

