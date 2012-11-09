rosbuild_add_library(ublox_gps gps.cpp)
rosbuild_link_boost(ublox_gps system)

rosbuild_add_executable(ublox_gps_node node.cpp)
rosbuild_link_boost(ublox_gps_node regex)
target_link_libraries(ublox_gps_node ublox_gps)
