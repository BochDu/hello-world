# 设置CMake的最低版本要求
cmake_minimum_required(VERSION 3.10)

# 设置项目名称
project(hello_world)

# 指定 C 编译器
set(CMAKE_C_COMPILER gcc)

# 指定 C++ 编译器
set(CMAKE_CXX_COMPILER g++)

# 设置C标准
set(CMAKE_C_STANDARD 11)

# 添加静态库
add_library(hello_world_product STATIC hello_world.c)

# 将头文件目录添加到包含路径
target_include_directories(hello_world_product PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# 移除搬运静态库到仓库根目录的命令
add_custom_command(TARGET hello_world_product POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:hello_world_product> ${CMAKE_SOURCE_DIR}/../hello_world.a
)