# 设置 CMake 最低版本要求
cmake_minimum_required(VERSION 3.10)

# 设置项目名称
project(DemoProject)

# 指定 C 编译器
set(CMAKE_C_COMPILER gcc)

# 指定 C++ 编译器
set(CMAKE_CXX_COMPILER g++)

# 设置 C 标准
set(CMAKE_C_STANDARD 11)

# 查找当前目录下所有的 .h 头文件
file(GLOB_RECURSE HEADER_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.h)

# 添加头文件搜索路径
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# 查找当前目录下所有的 .a 静态库文件
file(GLOB_RECURSE STATIC_LIBRARIES ${CMAKE_CURRENT_SOURCE_DIR}/*.a)

# 添加可执行文件
add_executable(demo demo.c)

# 链接静态库
target_link_libraries(demo PRIVATE ${STATIC_LIBRARIES})