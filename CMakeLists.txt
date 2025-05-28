cmake_minimum_required(VERSION 3.10)
project(QToDo VERSION 0.1.0)

# 设置C++标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 编译选项
if(MSVC)
    add_compile_options(/W4 /WX)
    # 添加安全CRT函数支持
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
else()
    add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# 包含目录
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

# Dear ImGui 依赖
add_subdirectory(vendor/imgui)
include_directories(vendor/imgui)

# 获取源文件
file(GLOB_RECURSE SOURCES "src/*.cpp")
file(GLOB_RECURSE HEADERS "include/*.h")

# 添加可执行文件
add_executable(QToDo ${SOURCES} ${HEADERS})

# 链接库
target_link_libraries(QToDo PRIVATE imgui)

# 复制资源文件到构建目录
file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/resources DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

# 安装规则
install(TARGETS QToDo DESTINATION bin)
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/resources/ DESTINATION bin/resources)
