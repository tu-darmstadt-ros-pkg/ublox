cmake_minimum_required(VERSION 2.8.3)
project(ublox_gps)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS roscpp ublox_msgs sensor_msgs ublox_serialization)

## System dependencies are found with CMake's conventions
find_package(Boost REQUIRED COMPONENTS system)

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
  DEPENDS Boost
  CATKIN_DEPENDS roscpp ublox_msgs sensor_msgs ublox_serialization
  INCLUDE_DIRS include
  LIBRARIES ublox_gps
)

###########
## Build ##
###########

include_directories(
  include
  ${Boost_INCLUDE_DIR}
  ${catkin_INCLUDE_DIRS}
)

add_library(ublox_gps SHARED src/gps.cpp)
add_dependencies(ublox_gps ${catkin_EXPORTED_TARGETS})
target_link_libraries(ublox_gps ${catkin_LIBRARIES} ${Boost_LIBRARIES})

add_executable(ublox_gps_node src/node.cpp)
set_target_properties(ublox_gps_node PROPERTIES OUTPUT_NAME ublox_gps)
target_link_libraries(ublox_gps_node ublox_gps ${catkin_LIBRARIES})

#############
## Install ##
#############

install(TARGETS ublox_gps ublox_gps_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/ublox_gps/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"
)
