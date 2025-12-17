cmake_minimum_required(VERSION 3.10)

project(turingdb-python)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

message(STATUS "Running pull.sh")
execute_process(
    COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/pull.sh
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    RESULT_VARIABLE PULL_RESULT
)

if(NOT PULL_RESULT EQUAL 0)
    message(FATAL_ERROR "Pull script failed with ${PULL_RESULT}")
endif()

message(STATUS "Running turingdb/dependencies.sh")
execute_process(
    COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/turingdb/dependencies.sh
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    RESULT_VARIABLE DEPENDENCIES_RESULT
)

if(NOT DEPENDENCIES_RESULT EQUAL 0)
    message(FATAL_ERROR "Dependencies script failed with ${DEPENDENCIES_RESULT}")
endif()

add_subdirectory(turingdb)
