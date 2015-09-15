cmake_minimum_required(VERSION 2.8.3)
project(moosros_tester)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES
  CATKIN_DEPENDS roscpp std_msgs
  DEPENDS
)

add_executable(counter src/counter.cpp)

add_dependencies(counter ${catkin_EXPORTED_TARGETS})

target_link_libraries(counter
  ${catkin_LIBRARIES}
)
