cmake_minimum_required(VERSION 2.8.3)
project(moosros)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
)

find_package(MOOS REQUIRED)

find_package(Boost REQUIRED COMPONENTS thread system)


message(STATUS "MOOS package: ${MOOS_INCLUDE_DIRS}")
include_directories(${MOOS_INCLUDE_DIRS})
#link_directories(${MOOS_LIBRARY_DIRS})
#set(LIBS ${LIBS} ${MOOS_LIBRARIES})

#INCLUDE(FindPackageMessage)

message("----------------------------------------------")
if(MOOS_FOUND)
  message("MOOS FOUND!")
else(MOOS_FOUND)
  message("MOOS NOT FOUND")
endif(MOOS_FOUND)
message("----------------------------------------------")


catkin_package(
  INCLUDE_DIRS
  LIBRARIES
  CATKIN_DEPENDS roscpp std_msgs
  DEPENDS
)

add_executable(Bridge
  src/MsgContainer.h
  src/MOOSNode.cpp
  src/Bridge.cpp
)

add_dependencies(Bridge ${catkin_EXPORTED_TARGETS})

target_link_libraries(Bridge
  ${Boost_LIBRARIES}
  ${catkin_LIBRARIES}
  MOOS
)
