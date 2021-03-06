cmake_minimum_required(VERSION 2.8.3)
project(moveit_ros_planning_interface)

if(NOT CMAKE_CONFIGURATION_TYPES AND NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

find_package(Eigen REQUIRED)
find_package(Boost REQUIRED thread date_time system filesystem program_options python)
find_package(PythonLibs)
find_package(catkin REQUIRED COMPONENTS
  moveit_ros_planning
  moveit_ros_warehouse
  moveit_ros_manipulation
  moveit_ros_move_group
  eigen_conversions
  tf
  roscpp
  actionlib
  rospy
  rosconsole
)

set(THIS_PACKAGE_INCLUDE_DIRS
  py_bindings_tools/include
  move_group_interface/include
)

catkin_python_setup()

catkin_package(
  LIBRARIES  
    moveit_move_group_interface
  INCLUDE_DIRS
    ${THIS_PACKAGE_INCLUDE_DIRS}
  CATKIN_DEPENDS
    moveit_ros_planning
    moveit_ros_warehouse 
    moveit_ros_manipulation
    moveit_ros_move_group
    )

include_directories(${THIS_PACKAGE_INCLUDE_DIRS} 
                    ${catkin_INCLUDE_DIRS})

include_directories(SYSTEM
                    ${EIGEN_INCLUDE_DIRS}
		    ${Boost_INCLUDE_DIRS}
                    ${PYTHON_INCLUDE_DIRS})
		  
link_directories(${Boost_LIBRARY_DIRS})
link_directories(${catkin_LIBRARY_DIRS})

add_subdirectory(py_bindings_tools)
add_subdirectory(move_group_interface)

install(DIRECTORY resources DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
