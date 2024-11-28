cmake_minimum_required(VERSION 3.30.0)
project(sort)
set(CMAKE_CXX_STANDARD 11)

include_directories(${PROJECT_SOURCE_DIR}/include)
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

#变量和目录设置
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)#动态库和exe都生成到此文件

#生成动态库
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LIST)
add_library(common    
    SHARED
    ${SRC_LIST}
)#将src中的内容生成动态库
target_include_directories(common
PUBLIC
${PROJECT_SOURCE_DIR}/include
)#动态库包含头文件库


#可执行文件
add_executable(
    my_sort
    test.cpp
)

#可执行文件包含头文件
target_include_directories(my_sort
PUBLIC
${PROJECT_SOURCE_DIR}/include
)#包含头文件库


#可执行文件链接动态库
target_link_libraries(my_sort
PUBLIC
common
)

