# http://ros.org/doc/groovy/api/catkin/html/user_guide/supposed.html
cmake_minimum_required(VERSION 2.8.3)
project(ublox_msgs)
# Load catkin and all dependencies required for this package
find_package(catkin REQUIRED COMPONENTS message_generation ublox_serialization)

include_directories(include ${catkin_INCLUDE_DIRS})

add_message_files(
  FILES
  AidALM.msg
  AidEPH.msg
  AidHUI.msg
  CfgANT.msg
  CfgCFG.msg
  CfgMSG.msg
  CfgNAV5.msg
  CfgPRT.msg
  CfgRATE.msg
  CfgSBAS.msg
  NavCLOCK.msg
  NavDGPS.msg
  NavDGPS_SV.msg
  NavDOP.msg
  NavPOSECEF.msg
  NavPOSLLH.msg
  NavSBAS.msg
  NavSBAS_SV.msg
  NavSOL.msg
  NavSTATUS.msg
  NavSVINFO.msg
  NavSVINFO_SV.msg
  NavTIMEGPS.msg
  NavTIMEUTC.msg
  NavVELECEF.msg
  NavVELNED.msg
  RxmALM.msg
  RxmEPH.msg
  RxmRAW.msg
  RxmRAW_SV.msg
  RxmSFRB.msg
  RxmSVSI.msg
  RxmSVSI_SV.msg
)

## Generate added messages and services with any dependencies listed here
generate_messages(
  DEPENDENCIES
)

add_library(ublox_msgs SHARED src/ublox_msgs.cpp)
add_dependencies(ublox_msgs ublox_msgs_gencpp)

## DEPENDS: system dependencies of this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## INCLUDE_DIRS: 
## LIBRARIES: libraries you create in this project that dependent projects also need
catkin_package(
    DEPENDS
    CATKIN_DEPENDS message_runtime ublox_serialization
    INCLUDE_DIRS include
    LIBRARIES ublox_msgs
)


#############
## Install ##
#############

install(TARGETS ublox_msgs
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/ublox/ include/ublox_msgs/
   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
   FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"
)
