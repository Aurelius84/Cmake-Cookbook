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
    target_compile_options(message PRIVATE -O3)  # 多依赖的所有文件生效
    set_source_files_properties(Message.cc PROPERTIES COMPILE_FLAGS -O2) # 单独指定某个文件的编译选项
    add_executable(test test.cc)
    # CXX_STANDARD会设置我们想要的标准。
    # CXX_EXTENSIONS告诉CMake，只启用ISO C++标准的编译器标志，而不使用特定编译器的扩展。
    # CXX_STANDARD_REQUIRED指定所选标准的版本。如果这个版本不可用，CMake将停止配置并出现错误。
    # 当这个属性被设置为OFF时，CMake将寻找下一个标准的最新版本，直到一个合适的标志。
    # 这意味着，首先查找C++14，然后是C++11，然后是C++98。（译者注：目前会从C++20或C++17开始查找）
    set_target_properties(test PROPERTIES CXX_STANDARD 14 CXX_EXTENSIONS OFF CXX_STANDARD_REQUIRED ON)
    target_link_libraries(test message)
else()
    add_executable(test test.cc ${_sources})
endif()