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
add_library(hello_world STATIC hello_world.c)

# 添加可执行文件
add_executable(demo demo.c)

# 链接静态库到可执行文件
target_link_libraries(demo PRIVATE hello_world)

# 添加自定义命令，在构建后将静态库拷贝到根目录并更改名称
add_custom_command(TARGET hello_world POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:hello_world> ${CMAKE_SOURCE_DIR}/hello_world.a
    COMMENT "Copying static library to project root directory with a new name"
)