# console bridge
set(BUILD_SHARED_LIBS
  OFF 
  CACHE BOOL 
  "Build console_bridge as static library"
)
add_subdirectory(console_bridge)

# tiny xml
option(TINYXML_USE_STL
  "TINYXML_USE_STL can be used to turn on STL support."
  ON
)

add_library(tinyXML STATIC
  "tinyxml/tinyxml.cpp"
  "tinyxml/tinyxmlerror.cpp"
  "tinyxml/tinyxmlparser.cpp"
)

target_include_directories(tinyXML
  PUBLIC
  tinyxml
)

if(TINYXML_USE_STL)
  target_compile_definitions(tinyXML
    PUBLIC
    TIXML_USE_STL
  )
endif()

if(CMAKE_BUILD_TYPE MATCHES Debug)
  target_compile_options(tinyXML
    PUBLIC
    -Wall
    -Wno-format
    -g
    -DDEBUG
  )
elseif(CMAKE_BUILD_TYPE MATCHES Release)
  target_compile_options(tinyXML
    PUBLIC
    -Wall 
    -Wno-unknown-pragmas 
    -Wno-format 
    -O3
  )
endif()
