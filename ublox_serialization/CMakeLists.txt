# http://ros.org/doc/groovy/api/catkin/html/user_guide/supposed.html
cmake_minimum_required(VERSION 2.8.3)
project(ublox_serialization)

# Load catkin and all dependencies required for this package
find_package(catkin REQUIRED COMPONENTS roscpp roscpp_serialization)

include_directories(include ${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})

## DEPENDS: system dependencies of this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## INCLUDE_DIRS: 
## LIBRARIES: libraries you create in this project that dependent projects also need
catkin_package(
    DEPENDS roscpp roscpp_serialization
    CATKIN_DEPENDS roscpp roscpp_serialization
    INCLUDE_DIRS include
    LIBRARIES
)


#############
## Install ##
#############

install(DIRECTORY include/ublox/
   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
   FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"
)
