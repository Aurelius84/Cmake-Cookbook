cmake_minimum_required(VERSION 3.16 FATAL_ERROR)

project(recipe-02 LANGUAGES CXX)


# add_library(message STATIC Message.cc)
# add_library(message SHARED Message.cc)

# add_executable(test test.cc)
# target_link_libraries(test message)


add_library(message_objs OBJECT Message.cc)
add_library(message_shared SHARED $<TARGET_OBJECTS:message_objs>)
add_library(message_static STATIC $<TARGET_OBJECTS:message_objs>)

add_executable(test test.cc)
target_link_libraries(test message_static)