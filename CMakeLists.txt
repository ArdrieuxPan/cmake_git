cmake_minimum_required(VERSION 3.10)
project(planning_main)
set(CMAKE_CXX_STANDARD 17)

# 设置生成目录——————————
# 生成的动态共享库需要和主函数cpp文件位于同一级目录(二进制文件同目录、cpp和文件夹同级别)
# set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)   # WINDOWS：动态库和编译二进制文件都放在指定路径
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)     # LINUX:动态库和编译二进制文件都放在指定路径
# set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY) LINUX指定静态库和bin文件


# 动态库————————————
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)



add_library(common                  # 将src文件夹下所有文件封装成名为common的共享库
SHARED                              
${SRC_LISTS}
)
target_include_directories(common   # 链接common共享库所需头文件
PUBLIC
${PROJECT_SOURCE_DIR}/include
)



# 可执行文件————————————
add_executable(planning_main planning_main.cpp) # 将主函数cpp文件分装成名为planning_main的可执行文件
target_include_directories(planning_main        # 链接可执行文件所需头文件
PUBLIC
${PROJECT_SOURCE_DIR}/include
)
target_link_libraries(planning_main             # 链接可执行文件所需共享库文件
PUBLIC
common
)