cmake_minimum_required(VERSION 3.10)

# 设置项目名称
project(CMAKE_FIRST)

# 指定 C++ 标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 添加 include 目录
include_directories(include)

# 查找 src 和 code 目录下的所有 cpp 文件
file(GLOB SRC_FILES "src/*.cpp")
file(GLOB CODE_FILES "code/*.cpp")

# 生成可执行文件
add_executable(${PROJECT_NAME} ${SRC_FILES} ${CODE_FILES})
