# CMakeLists.txt
cmake_minimum_required (VERSION 3.8.2)
project (gpmf-parser)

set(CMAKE_SUPPRESS_REGENERATION true)
set(CMAKE_CONFIGURATION_TYPES "Debug;Release")

file(GLOB SOURCES "demo/*.c")

add_library(gpmf SHARED GPMF_parser.c)
add_executable(gpmf-parser ${SOURCES})
target_link_libraries(gpmf-parser gpmf)

set(include_dest "include")
set(lib_dest "lib")

install(TARGETS gpmf-parser DESTINATION bin)
install(TARGETS gpmf EXPORT gpmf DESTINATION "${lib_dest}")
install(FILES GPMF_parser.h DESTINATION "${include_dest}")
install(EXPORT gpmf DESTINATION lib/cmake/gpmf)

target_include_directories(gpmf PUBLIC
    $<BUILD_INTERFACE:${gpmf-parser_SOURCE_DIR}>
    $<INSTALL_INTERFACE:${include_dest}>
    $<INSTALL_INTERFACE:${lib_dest}>
)
