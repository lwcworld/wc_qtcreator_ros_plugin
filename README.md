# wc_qtcreator_ros_plugin
Qtcreator-ROS-Plugin install guide
===================================================
Prerequisites
------
- QT-ROS installation file download (https://ros-industrial.github.io/ros_qtc_plugin/_source/How-to-Install-Users.html)
- or clone this git repository

installation guide (http://blog.rovitek.com/44)
------
- right click on the file
- go to 'properties' tab
- check 'Execute: Allow executing file as program'
- double click the file to install

making ROS package
------
Create Workspace
- 'File' -> 'New File or Project'
- 'Other Project' tab
- select 'ROS Workspace' 
- set workspace name : 'ros_test'
- set Workspace Path : '/home/lwcworld/catkin_ws'
- 'Finish'

Make ROS pacakage
- right click on 'ros_test'
- 'Add New'
- set package name 'wc_world'
- in Dependencies ->  Catkin, write 'std_msgs roscpp rospy'
- Finish

Add .cpp source code
- right click 'wc_world'
- click 'Show Containing Folder'
- add new directory 'src', 'include'
- click 'Filter Tree' to see 'Hide Empty Directories'
- add new .cpp file in 'src' folder (wc_world_node.cpp)

Editing package.xml and CMakeList.txt
- 'pacakge.xml' example
```
<buildtool_depend>catkin</buildtool_depend>  
      
<build_depend>std_msgs</build_depend>  
<build_depend>roscpp</build_depend>  
      
<exec_depend>std_msgs</exec_depend>  
<exec_depend>roscpp</exec_depend>  
```

- 'CMakeList.txt' example
```
cmake_minimum_required(VERSION 2.8.3)  
project(hello_world)  
      
      
find_package(catkin REQUIRED COMPONENTS  
  std_msgs roscpp  
)  
      
      
catkin_package(  
#  INCLUDE_DIRS include  
  LIBRARIES hello_world  
  CATKIN_DEPENDS std_msgs roscpp  
  DEPENDS system_lib  
)  
      
include_directories(  
# include  
  ${catkin_INCLUDE_DIRS}  
)  
      
add_executable(hello_world_node src/hello_world_node.cpp)  
add_dependencies(hello_world_node hello_world_generate_messages_cpp)  
target_link_libraries(hello_world_node ${catkin_LIBRARIES})  
```

Project setting
- default setting is to build all the packages in the workspace(catkin_ws) which means consume large time
- let's set to build only one package
- go to 'Projects' tab on the left
- go to 'Build', expand 'Build Steps' and 'Clean Steps, set 'CatkinTools Arguments' as package name ('wc_world')
- go to 'Run', expand 'Run' and set 'Package' and 'Target' as 'wc_world' and 'wc_world_node'

Execution
- 'ROS terminal' is needed
- run 'roscore'
- build using 'Ctrl + R' or 'Build -> Run'

