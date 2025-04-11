# 设置CMake的最低版本要求
cmake_minimum_required(VERSION 3.10)

# 设置项目名称的变量
set(PROJECT_NAME_VAR hello_world)

# 设置项目名称
project(${PROJECT_NAME_VAR})

# 指定 C 编译器
set(CMAKE_C_COMPILER gcc)

# 指定 C++ 编译器
set(CMAKE_CXX_COMPILER g++)

# 设置C标准
set(CMAKE_C_STANDARD 11)

# 添加静态库
add_library(${PROJECT_NAME_VAR} STATIC ${PROJECT_NAME_VAR}.c)

# 将头文件目录添加到包含路径
target_include_directories(${PROJECT_NAME_VAR} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# 移除搬运静态库到仓库根目录的命令
add_custom_command(TARGET ${PROJECT_NAME_VAR} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:${PROJECT_NAME_VAR}> ${CMAKE_SOURCE_DIR}/../${PROJECT_NAME_VAR}.a
)

# 使用 file(GLOB) 收集所有的 .h 文件
file(GLOB HEADER_FILES "${CMAKE_CURRENT_SOURCE_DIR}/*.h")

# 搬运当前目录下所有的 .h 文件到上级目录
foreach(HEADER_FILE ${HEADER_FILES})
    add_custom_command(TARGET ${PROJECT_NAME_VAR} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E echo "Copying file: ${HEADER_FILE} to ${CMAKE_SOURCE_DIR}/.."
        COMMAND ${CMAKE_COMMAND} -E copy_if_different ${HEADER_FILE} ${CMAKE_SOURCE_DIR}/..
    )
endforeach()