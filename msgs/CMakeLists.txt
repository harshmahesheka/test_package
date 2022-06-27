#
# Development of this module has been funded by the Monterey Bay Aquarium
# Research Institute (MBARI) and the David and Lucile Packard Foundation
#

find_package(Protobuf REQUIRED)

ign_add_msgs(${CMAKE_CURRENT_SOURCE_DIR} COMMON_LANGUAGE cpp 
                  COMMON_IMPORT_DIRS  ${ignition-msgs${IGN_MSGS_VER}_INCLUDE_DIRS} 
                  COMMON_PROTOC_OUT_DIR ${CMAKE_BINARY_DIR}/msgs)



