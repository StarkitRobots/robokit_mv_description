cmake_minimum_required(VERSION 2.8.3)

project(robokit_mv_description)

find_package(catkin REQUIRED COMPONENTS  rospy message_generation std_msgs webots_ros) # ros webots??
add_message_files(
  FILES
  servo_command.msg
)
generate_messages(
  DEPENDENCIES
  std_msgs
)
catkin_package(#  INCLUDE_DIRS include
#  LIBRARIES webots_ros
  CATKIN_DEPENDS rospy
#  DEPENDS system_lib
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)
find_package(roslaunch)
catkin_install_python(PROGRAMS
  scripts/motion_atom.py
  scripts/servo_control.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
foreach(dir config launch meshes urdf scripts)
	install(DIRECTORY ${dir}/
		DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach(dir)
