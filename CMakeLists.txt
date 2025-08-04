cmake_minimum_required(VERSION 3.26)
project(VulkanProject)

set(CMAKE_CXX_STANDARD 17)

add_executable(${PROJECT_NAME} main.cpp)

set(GLFW_DIR "C:/Libs/GLFW")
set(VULKAN_SDK_PATH "C:/VulkanSDK/1.4.313.2")
set(STB_IMAGE_DIR "C:/Libs/STB_IMAGE")
set(TINY_OBJ_LOADER "C:/Libs/TINY_OBJ_LOADER")

include_directories(${GLFW_DIR}/include)
include_directories(${VULKAN_SDK_PATH}/Include)
include_directories(${STB_IMAGE_DIR})
include_directories(${TINY_OBJ_LOADER})

target_link_directories(${PROJECT_NAME} PUBLIC ${VULKAN_SDK_PATH}/Lib)
target_link_directories(${PROJECT_NAME} PUBLIC ${GLFW_DIR}/lib-mingw-w64)

target_link_libraries(${PROJECT_NAME} vulkan-1)
target_link_libraries(${PROJECT_NAME} glfw3)

set(SETUP_SCRIPT ${CMAKE_SOURCE_DIR}/setup.bat)

add_custom_target(run_setup
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
        COMMAND ${CMAKE_COMMAND} -E env cmd /c ${SETUP_SCRIPT}
        VERBATIM
)

add_dependencies(${PROJECT_NAME} run_setup)