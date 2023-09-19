cmake_minimum_required(VERSION 3.16 FATAL_ERROR)
project(recipe-02 LANGUAGES CXX)  # <--- 此处为 NONE


add_executable(test test.cc)

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    message(STATUS "on Linux")
    # 通过使用target_compile_definition在预处理阶段使用
    target_compile_definitions(test PUBLIC "IS_LINUX")
elseif(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
    message(STATUS "on MacOS")
    target_compile_definitions(test PUBLIC "IS_MACOS")
elseif(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    message(STATUS "on Windows")
    target_compile_definitions(test PUBLIC "IS_WINDOWS")
endif()


# 注：target_compile_definitions 相对于add_definitions的优点
# 1. 将定义限制于一个特定的目标，以及通过 PRIVATE|PUBLIC|INTERFACE限定符，限制这些定义可见性

# PRIVATE，编译定义将只应用于给定的目标，而不应用于相关的其他目标。
# INTERFACE，对给定目标的编译定义将只应用于使用它的目标。
# PUBLIC，编译定义将应用于给定的目标和使用它的所有其他目标。