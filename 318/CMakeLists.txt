cmake_minimum_required(VERSION 3.10)

# 设置项目名称
set(PROJECT_N MyProject)
project(${PROJECT_N} VERSION 1.0)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 递归查找 src 目录中的 .cpp 源文件
file(GLOB_RECURSE SRCS ${PROJECT_SOURCE_DIR}/src/*.cpp)

# 宏：获取所有包含头文件的目录（支持 .h 和 .hpp）
MACRO(header_directories return_list includes_base_folder)
    FILE(GLOB_RECURSE hpp_list ${includes_base_folder}/*.hpp)
    FILE(GLOB_RECURSE h_list ${includes_base_folder}/*.h)
    SET(new_list ${hpp_list} ${h_list})
    SET(dir_list "")
    FOREACH(file_path ${new_list})
        GET_FILENAME_COMPONENT(dir_path ${file_path} PATH)
        SET(dir_list ${dir_list} ${dir_path})
    ENDFOREACH()
    LIST(REMOVE_DUPLICATES dir_list)
    SET(${return_list} ${dir_list})
ENDMACRO()

# 运行宏，获取 include 目录的头文件路径
header_directories(INCLUDES ${PROJECT_SOURCE_DIR}/include)

# 输出调试信息
message("Source files:")
foreach(file ${SRCS})
    message(STATUS ${file})
endforeach()

message("Include directories:")
foreach(dir ${INCLUDES})
    message(STATUS ${dir})
endforeach()

# 生成可执行文件
add_executable(${PROJECT_N} ${SRCS})

# 添加 include 目录
target_include_directories(${PROJECT_N} PUBLIC ${INCLUDES})
