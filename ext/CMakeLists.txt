# console bridge
add_subdirectory(console_bridge)

# tiny xml
add_library(tinyXML STATIC
  "tinyxml/tinyxml.cpp"
  "tinyxml/tinyxmlerror.cpp"
  "tinyxml/tinyxmlparser.cpp"
)

target_include_directories(tinyXML
  PUBLIC
  tinyxml
)

target_compile_definitions(tinyXML
  PRIVATE
  TIXML_USE_STL
  _CRT_SECURE_NO_DEPRECATE
  _CRT_NONSTDC_NO_DEPRECATE
  INTERFACE
  TIXML_USE_STL
)