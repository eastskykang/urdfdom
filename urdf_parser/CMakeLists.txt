add_library(urdfdom_world SHARED src/pose.cpp src/model.cpp src/link.cpp src/joint.cpp src/world.cpp)
target_link_libraries(urdfdom_world 
  tinyXML 
  console_bridge
)
target_include_directories(urdfdom_world
  PUBLIC
  "include"
  PRIVATE
  urdf_exception
  urdf_model
  urdf_model_state
  urdf_sensor
  urdf_world
)
set_target_properties(urdfdom_world PROPERTIES SOVERSION ${URDF_MAJOR_MINOR_VERSION})

add_library(urdfdom_model SHARED src/pose.cpp src/model.cpp src/link.cpp src/joint.cpp)
target_link_libraries(urdfdom_model 
  tinyXML
  console_bridge
)
target_include_directories(urdfdom_model
  PUBLIC
  "include"
  PRIVATE
  urdf_exception
  urdf_model
  urdf_model_state
  urdf_sensor
  urdf_world
)
set_target_properties(urdfdom_model PROPERTIES SOVERSION ${URDF_MAJOR_MINOR_VERSION})

add_library(urdfdom_sensor SHARED src/urdf_sensor.cpp)
target_link_libraries(urdfdom_sensor 
  urdfdom_model 
  tinyXML
  console_bridge
)
target_include_directories(urdfdom_sensor 
  PUBLIC
  "include"
  PRIVATE
  urdf_exception
  urdf_model
  urdf_model_state
  urdf_sensor
  urdf_world
)
set_target_properties(urdfdom_sensor PROPERTIES SOVERSION ${URDF_MAJOR_MINOR_VERSION})

add_library(urdfdom_model_state SHARED src/urdf_model_state.cpp src/twist.cpp)
target_link_libraries(urdfdom_model_state 
  tinyXML
  console_bridge
)
target_include_directories(urdfdom_model_state 
  PUBLIC
  "include"
  PRIVATE
  urdf_exception
  urdf_model
  urdf_model_state
  urdf_sensor
  urdf_world
)
set_target_properties(urdfdom_model_state PROPERTIES SOVERSION ${URDF_MAJOR_MINOR_VERSION})

# --------------------------------

add_executable(check_urdf src/check_urdf.cpp)
target_link_libraries(check_urdf urdfdom_model urdfdom_world)

add_executable(urdf_to_graphiz src/urdf_to_graphiz.cpp)
target_link_libraries(urdf_to_graphiz urdfdom_model)