cmake_minimum_required(VERSION 3.10.2 FATAL_ERROR)

project(test_package)

find_package(ignition-cmake2 REQUIRED)
find_package(Protobuf REQUIRED)
find_package(Protobuf REQUIRED)
find_package(ignition-gazebo6 REQUIRED)
set(IGN_GAZEBO_VER ${ignition-gazebo6_VERSION_MAJOR})
find_package(ignition-common4 REQUIRED COMPONENTS graphics)
set(IGN_COMMON_VER ${ignition-common4_VERSION_MAJOR})
find_package(ignition-fuel_tools7 REQUIRED)
find_package(ignition-math6 REQUIRED)
set(IGN_MATH_VER ${ignition-math6_VERSION_MAJOR})
find_package(ignition-msgs8 REQUIRED)
set(IGN_MSGS_VER ${ignition-msgs8_VERSION_MAJOR})
find_package(ignition-transport11 REQUIRED)
find_package(ignition-plugin1 REQUIRED COMPONENTS loader register)
set(IGN_PLUGIN_VER ${ignition-plugin1_VERSION_MAJOR})
find_package(ignition-rendering6 REQUIRED)
set(IGN_RENDERING_VER ${ignition-rendering6_VERSION_MAJOR})
find_package(sdformat12 REQUIRED)
find_package(ignition-gui6 REQUIRED)
set(IGN_GUI_VER ${ignition-gui6_VERSION_MAJOR})
find_package(ignition-utils1 REQUIRED)
set(IGN_UTILS_VER ${ignition-utils1_VERSION_MAJOR})

##New Macros

ign_add_resources(worlds)
ign_add_resources(models)
ign_add_plugins(plugins COMMON_PUBLIC_LIBRARIES 
 ignition-gazebo${IGN_GAZEBO_VER}::ignition-gazebo${IGN_GAZEBO_VER}
 ignition-common${IGN_COMMON_VER}::ignition-common${IGN_COMMON_VER}
 ignition-plugin${IGN_PLUGIN_VER}::ignition-plugin${IGN_PLUGIN_VER})
ign_add_executables(examples COMMON_PUBLIC_LIBRARIES 
 ignition-gazebo${IGN_GAZEBO_VER}::ignition-gazebo${IGN_GAZEBO_VER})
ign_export_variable(LD_LIBRARY_PATH @CMAKE_INSTALL_PREFIX@/lib)
ign_add_plugins(gui_plugins COMMON_PUBLIC_LIBRARIES
ignition-rendering${IGN_RENDERING_VER}::ignition-rendering${IGN_RENDERING_VER}  GUI true)
ign_add_msgs(msgs COMMON_LANGUAGE cpp 
                  COMMON_IMPORT_DIRS  ${ignition-msgs${IGN_MSGS_VER}_INCLUDE_DIRS} 
                  COMMON_PROTOC_OUT_DIR ${CMAKE_BINARY_DIR})
ign_environment_hook(colcon)

################

if(BUILD_TESTING)

  # Build-time constants
  set("PROJECT_BINARY_PATH" ${CMAKE_CURRENT_BINARY_DIR})
  set("PROJECT_SOURCE_PATH" ${CMAKE_CURRENT_SOURCE_DIR})
  
endif()


