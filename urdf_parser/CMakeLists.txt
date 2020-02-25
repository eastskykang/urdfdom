# dependencies
# urdfdom headers
set(URDFDOM_HEADER_INCLUDE_DIRS
  ${CMAKE_CURRENT_SOURCE_DIR}/../ext/urdfdom_headers/urdf_exception/include
  ${CMAKE_CURRENT_SOURCE_DIR}/../ext/urdfdom_headers/urdf_model/include
  ${CMAKE_CURRENT_SOURCE_DIR}/../ext/urdfdom_headers/urdf_model_state/include
  ${CMAKE_CURRENT_SOURCE_DIR}/../ext/urdfdom_headers/urdf_sensor/include
  ${CMAKE_CURRENT_SOURCE_DIR}/../ext/urdfdom_headers/urdf_world/include
)

# console bridge
set(CONSOLE_BRIDGE_INCLUDE_DIRS
  ${CMAKE_CURRENT_SOURCE_DIR}/../ext/console_bridge/include
  ${CMAKE_CURRENT_BINARY_DIR}/../ext/console_bridge
)

#--------------------------------------------------------------------------------
# urdfdom_world
add_library(urdfdom_world SHARED 
  src/pose.cpp 
  src/model.cpp 
  src/link.cpp 
  src/joint.cpp 
  src/world.cpp
)

target_include_directories(urdfdom_world
  PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  ${URDFDOM_HEADER_INCLUDE_DIRS}
  ${CONSOLE_BRIDGE_INCLUDE_DIRS}
)

target_link_libraries(urdfdom_world 
  tinyXML 
  console_bridge
)

set_target_properties(urdfdom_world 
  PROPERTIES 
  SOVERSION ${URDF_MAJOR_MINOR_VERSION}
)

# urdfdom_model
add_library(urdfdom_model SHARED 
  src/pose.cpp 
  src/model.cpp 
  src/link.cpp 
  src/joint.cpp
)

target_link_libraries(urdfdom_model 
  tinyXML
  console_bridge
)

target_include_directories(urdfdom_model
  PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  ${URDFDOM_HEADER_INCLUDE_DIRS}
  ${CONSOLE_BRIDGE_INCLUDE_DIRS})

set_target_properties(urdfdom_model 
  PROPERTIES SOVERSION 
  ${URDF_MAJOR_MINOR_VERSION}
)

# urdfdom_sensor
add_library(urdfdom_sensor SHARED 
  src/urdf_sensor.cpp
)

target_link_libraries(urdfdom_sensor 
  urdfdom_model 
  tinyXML
  console_bridge
)

target_include_directories(urdfdom_sensor 
  PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  ${URDFDOM_HEADER_INCLUDE_DIRS}
  ${CONSOLE_BRIDGE_INCLUDE_DIRS}
)

set_target_properties(urdfdom_sensor 
  PROPERTIES 
  SOVERSION ${URDF_MAJOR_MINOR_VERSION}
)

# urdfdom_model_state
add_library(urdfdom_model_state SHARED 
  src/urdf_model_state.cpp 
  src/twist.cpp
)

target_link_libraries(urdfdom_model_state 
  tinyXML
  console_bridge
)

target_include_directories(urdfdom_model_state 
  PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  ${URDFDOM_HEADER_INCLUDE_DIRS}
  ${CONSOLE_BRIDGE_INCLUDE_DIRS}
)

set_target_properties(urdfdom_model_state 
  PROPERTIES 
  SOVERSION ${URDF_MAJOR_MINOR_VERSION}
)

# --------------------------------

add_executable(check_urdf src/check_urdf.cpp)
target_link_libraries(check_urdf urdfdom_model urdfdom_world)

add_executable(urdf_to_graphiz src/urdf_to_graphiz.cpp)
target_link_libraries(urdf_to_graphiz urdfdom_model)