cmake_minimum_required(VERSION 3.16 FATAL_ERROR)
project(recipe-03 LANGUAGES CXX)

# set(USE_LIB OFF)
option(USE_LIB "Whether to use lib" OFF) # cmake .. -DUSE_LIB=ON
message(STATUS "USE_LIB: ${USE_LIB}")

include(CMakeDependentOption)
cmake_dependent_option(MAKE_STATIC_LIBRARY "Compile sources into static lib" OFF "USE_LIB" ON)


set(BUILD_SHARED_LIB OFF)   # cmake global flag

list(APPEND _sources Message.cc)

if(USE_LIB)
    add_library(message ${_sources})
    add_executable(test test.cc)
    target_link_libraries(test message)
else()
    add_executable(test test.cc ${_sources})
endif()