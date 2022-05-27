cmake_minimum_required(VERSION 3.10.2 FATAL_ERROR)

project(test_package)

find_package(ignition-cmake2 REQUIRED)

find_package(ign_gazebo_dev REQUIRED)
# set(IGN_GAZEBO_VER ${ignition-gazebo6_VERSION_MAJOR})
find_package(ignition-common4 REQUIRED COMPONENTS graphics)
set(IGN_COMMON_VER ${ignition-common4_VERSION_MAJOR})
find_package(ignition-fuel_tools7 REQUIRED)
find_package(ignition-math6 REQUIRED)
set(IGN_MATH_VER ${ignition-math6_VERSION_MAJOR})
find_package(ignition-msgs8 REQUIRED)
find_package(ignition-transport11 REQUIRED)
find_package(ignition-plugin1 REQUIRED COMPONENTS loader register)
set(IGN_PLUGIN_VER ${ignition-plugin1_VERSION_MAJOR})
find_package(ignition-rendering6 REQUIRED)
set(IGN_RENDERING_VER ${ignition-rendering6_VERSION_MAJOR})
find_package(sdformat12 REQUIRED)

find_package(ignition-utils1 REQUIRED)
set(IGN_UTILS_VER ${ignition-utils1_VERSION_MAJOR})

#============================================================================
# Hooks
configure_file(
  "hooks/hook.dsv.in"
  "${CMAKE_CURRENT_BINARY_DIR}/hooks/hook.dsv" @ONLY
)

# Add sources for each plugin to be registered.

add_library(HelloWorld SHARED plugins/HelloWorld)
set_property(TARGET HelloWorld PROPERTY CXX_STANDARD 17)
target_link_libraries(HelloWorld PUBLIC
  ignition-gazebo${IGN_GAZEBO_VER}::ignition-gazebo${IGN_GAZEBO_VER}
  ignition-common${IGN_COMMON_VER}::ignition-common${IGN_COMMON_VER}
  ignition-plugin${IGN_PLUGIN_VER}::ignition-plugin${IGN_PLUGIN_VER}
)
install(
  TARGETS HelloWorld
  DESTINATION lib)

# Resources
install(DIRECTORY
  worlds
  models
  launch
  ${CMAKE_CURRENT_BINARY_DIR}/hooks
  DESTINATION share/${PROJECT_NAME})

if(BUILD_TESTING)


  # Build-time constants
  set("PROJECT_BINARY_PATH" ${CMAKE_CURRENT_BINARY_DIR})
  set("PROJECT_SOURCE_PATH" ${CMAKE_CURRENT_SOURCE_DIR})



  
endif()


