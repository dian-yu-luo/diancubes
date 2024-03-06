cmake_minimum_required(VERSION 3.10)

project(DianCubes)

set(CMAKE_CXX_STANDARD 17)

if(MSVC)
    add_compile_options(/wd4819)
endif()


link_directories(lib)

# 添加 GLAD 和链接 OpenGL 库
include_directories(include)
# 添加源文件
set(SOURCE_FILES 
    src/main.cpp
    src/glad.c
    # 这里列出你的其他源文件
)

# 创建可执行文件
add_executable(DianCubes ${SOURCE_FILES})

# 链接 GLFW 和 GLAD 库
target_link_libraries(DianCubes PRIVATE glfw3 )

