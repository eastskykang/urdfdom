# console bridge
add_subdirectory(console_bridge)

# urdfdom headers
# urdf_exception
add_library(urdf_exception INTERFACE)
target_include_directories(urdf_exception INTERFACE "urdfdon_headers/urdf_exception/include")
# urdf_model
add_library(urdf_model INTERFACE)
target_include_directories(urdf_exception INTERFACE "urdfdon_headers/urdf_model/include")
# urdf_model_state
add_library(urdf_model_state INTERFACE)
target_include_directories(urdf_exception INTERFACE "urdfdon_headers/urdf_model_state/include")
# urdf_sensor
add_library(urdf_sensor INTERFACE)
target_include_directories(urdf_exception INTERFACE "urdfdon_headers/urdf_sensor/include")
# urdf_world
add_library(urdf_world INTERFACE)
target_include_directories(urdf_exception INTERFACE "urdfdon_headers/urdf_world/include")

# tiny xml
add_library(tinyXML STATIC
  "tinyxml/tinyxml.h"
  "tinyxml/tinyxml.cpp"
  "tinyxml/tinyxmlerror.cpp"
  "tinyxml/tinyxmlparser.cpp"
)

target_compile_definitions(tinyXML
  PRIVATE
  TIXML_USE_STL
  _CRT_SECURE_NO_DEPRECATE
  _CRT_NONSTDC_NO_DEPRECATE
  INTERFACE
  TIXML_USE_STL
)