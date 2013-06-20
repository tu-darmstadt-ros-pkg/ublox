# http://ros.org/doc/groovy/api/catkin/html/user_guide/supposed.html
cmake_minimum_required(VERSION 2.8.3)
project(ublox_gps)

# Load catkin and all dependencies required for this package
find_package(catkin REQUIRED COMPONENTS roscpp ublox_msgs sensor_msgs ublox_serialization)
find_package(Boost REQUIRED COMPONENTS system)

include_directories(include ${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})

add_library(ublox_gps SHARED src/gps.cpp)
target_link_libraries(ublox_gps ${catkin_LIBRARIES} ${Boost_LIBRARIES})

add_executable(ublox_gps_node src/node.cpp)
set_target_properties(ublox_gps_node PROPERTIES OUTPUT_NAME ublox_gps)
target_link_libraries(ublox_gps_node ublox_gps ${catkin_LIBRARIES})

## DEPENDS: system dependencies of this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## INCLUDE_DIRS: 
## LIBRARIES: libraries you create in this project that dependent projects also need
catkin_package(
    DEPENDS boost
    CATKIN_DEPENDS roscpp ublox_msgs sensor_msgs ublox_serialization
    INCLUDE_DIRS include
    LIBRARIES ublox_gps
)

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
