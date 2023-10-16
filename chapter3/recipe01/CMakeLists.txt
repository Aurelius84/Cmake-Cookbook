cmake_minimum_required(VERSION 3.16 FATAL_ERROR)
project(recipe-01 LANGUAGES NONE)

find_package(PythonInterp REQUIRED)

execute_process(
    COMMAND ${PYTHON_EXECUTABLE} "-c" "print('hello world')"  # DO NOT USE "-c print('hello world')"
    RESULT_VARIABLE _status
    OUTPUT_VARIABLE _hello_world
    ERROR_QUIET
    OUTPUT_STRIP_TRAILING_WHITESPACE   
)

message(STATUS ${_status})  # 0
message(STATUS ${_hello_world}) # hello world


# 工作原理：
# find_package是用于发现和设置包的CMake模块的命令。
# 这些模块包含CMake命令，用于标识系统标准位置中的包。CMake模块文件称为 Find<name>.cmake，当调用find_package(<name>)时，模块中的命令将会运行。
# 对于Python解释器，相关模块为FindPythonInterp.cmake附带的设置了一些CMake变量:

# PYTHONINTERP_FOUND：是否找到解释器
# PYTHON_EXECUTABLE：Python解释器到可执行文件的路径
# PYTHON_VERSION_STRING：Python解释器的完整版本信息
# PYTHON_VERSION_MAJOR：Python解释器的主要版本号
# PYTHON_VERSION_MINOR ：Python解释器的次要版本号
# PYTHON_VERSION_PATCH：Python解释器的补丁版本号

# 软件包没有安装在标准位置时，CMake无法正确定位它们。用户可以使用CLI的-D参数传递相应的选项，告诉CMake查看特定的位置。Python解释器可以使用以下配置:
# cmake -D PYTHON_EXECUTABLE=/custom/location/python ..

# 可以借助 help 模块：
# cmake --help-module FindPythonInterp