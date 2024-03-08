cmake_minimum_required(VERSION 3.10)

project(DianCubes)

set(CMAKE_CXX_STANDARD 17)

if(MSVC)
    add_compile_options(/wd4819)
endif()

# 添加资源目录
set(RESOURCES_DIR ${PROJECT_SOURCE_DIR}/res)
file(GLOB_RECURSE RESOURCES ${RESOURCES_DIR}/*)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/out/)

# 将资源复制到输出目录
foreach(RESOURCE ${RESOURCES})
file(RELATIVE_PATH RESOURCE_PATH ${RESOURCES_DIR} ${RESOURCE})
configure_file(${RESOURCE} ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${RESOURCE_PATH}
COPYONLY)
endforeach()


# 依靠fetchcontent 属性安装第三方库
include(FetchContent)

FetchContent_Declare(
  glm
  GIT_REPOSITORY https://github.com/g-truc/glm.git
  GIT_TAG 1.0.1
  GIT_SHALLOW 1
  )

FetchContent_MakeAvailable(glm)

# FetchContent_Declare(
#   json
#   GIT_REPOSITORY https://github.com/nlohmann/json.git
#   GIT_TAG v3.11.1)

# FetchContent_MakeAvailable(json)


link_directories(lib)

# 添加 GLAD 和链接 OpenGL 库
include_directories(include)
# 添加源文件
set(SOURCE_FILES 
    src/main.cpp
    src/glad.c
    src/stb_image.cpp
    # 这里列出你的其他源文件
)

# 创建可执行文件
add_executable(DianCubes ${SOURCE_FILES})

# 链接 GLFW 和 GLAD 库
target_link_libraries(DianCubes PRIVATE glfw3 glm)

