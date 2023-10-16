cmake_minimum_required(VERSION 3.16 FATAL_ERROR)
project(recipe-02 LANGUAGES C)

# set(CMAKE_C_STANDARD 99)
# set(CMAKE_C_EXTENSIONS OFF)
# set(CMAKE_C_STANDARD_REQUIRED ON)

find_package(PythonInterp REQUIRED)
find_package(PythonLibs ${PYTHON_VERSION_MAJOR}.${PYTHON_VERSION_MINOR} EXACT REQUIRED)

add_executable(test test.c)
target_include_directories(test PRIVATE ${PYTHON_INCLUDE_DIRS})
message(STATUS ${PYTHON_INCLUDE_DIRS})
target_link_libraries(test PRIVATE ${PYTHON_LIBRARIES})