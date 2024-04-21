cmake_minimum_required(VERSION 3.10)
set(CMAKE_CXX_STANDARD 17)
project(planning_test)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LIST)
include_directories(${PROJECT_SOURCE_DIR}/include)

add_executable(planning_test
    ${SRC_LIST}
)