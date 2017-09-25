cmake_minimum_required(VERSION 2.8.3)
project(ras_group8_motor_controller)

find_package(catkin REQUIRED
	COMPONENTS
	roscpp
	geometry_msgs
)

catkin_package(
	INCLUDE_DIRS
		include
	
	CATKIN_DEPENDS
		roscpp
		geometry_msgs
	
# DEPENDS
)

include_directories(
	include
	${catkin_INCLUDE_DIRS}
)

add_executable(${PROJECT_NAME}
	src/motor_controller_node.cpp
	src/motor_controller.cpp
)

add_dependencies(${PROJECT_NAME}
	${catkin_EXPORTED_TARGETS}
)

target_link_libraries(${PROJECT_NAME}
	${catkin_LIBRARIES}
)

#catkin_add_gtest(motor_controller_tests test/motor_controller_test.cpp src/motor_controller.cpp)

# Make main executable
install(
  TARGETS ${PROJECT_NAME}
	ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
	LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
	RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

# Install headers
install(
  DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.hpp"
)