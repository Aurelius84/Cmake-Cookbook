cmake_minimum_required(VERSION 3.16 FATAL_ERROR)
project(recipe-01 LANGUAGES NONE)  # <--- 此处为 NONE

#<<< 如果检测系统， CMake为目标操作系统定义了CMAKE_SYSTEM_NAME，
# 因此不需要使用定制命令、工具或脚本来查询此信息。
if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    message(STATUS "on Linux")
elseif(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
    message(STATUS "on MacOS")
elseif(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    message(STATUS "on Windows")
elseif(CMAKE_SYSTEM_NAME STREQUAL "AIX")
    message(STATUS "on IBM AIX")
else()
    message(STATUS "for ${CMAKE_SYSTEM_NAME}")
endif()


# 输出：
# -- on MacOS
# -- Configuring done (0.1s)
# -- Generating done (0.0s)


# 注：为了最小化从一个平台转移到另一个平台时的成本，应该避免直接使用Shell命令，
# 还应该避免显式的路径分隔符(Linux和macOS上的前斜杠和Windows上的后斜杠)。
# CMake代码中只使用前斜杠作为路径分隔符，CMake将自动将它们转换为所涉及的操作系统环境。
