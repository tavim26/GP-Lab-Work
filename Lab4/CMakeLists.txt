cmake_minimum_required(VERSION 3.16)

project(test LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(GLM_DIR "/usr/share/cmake/glm")

set(GLEW_DIR "/usr/include/GL")
set(GLEW_LIBS "/usr/lib64/libGLEW.so")

set(GLFW_DIR "/usr/include/GLFW")
set(GLFW_LIBS "/usr/lib64/libglfw.so")

# Include OpenGL
find_package(OpenGL REQUIRED)

include_directories(
        ${GLM_DIR}
        ${GLEW_DIR}
        ${GLFW_DIR}
)

add_executable(${PROJECT_NAME} main.cpp
        main.cpp
        Shader.cpp)

target_include_directories(${PROJECT_NAME} PRIVATE ${GLM_DIR} ${GLEW_DIR} ${GLFW_DIR})

# Link the necessary libraries, including OpenGL
target_link_libraries(${PROJECT_NAME} PRIVATE ${GLEW_LIBS} ${GLFW_LIBS} OpenGL::GL)

include(GNUInstallDirs)
install(TARGETS ${PROJECT_NAME}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)