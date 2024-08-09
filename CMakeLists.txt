cmake_minimum_required(VERSION 3.26)
project(VulkanTriangle)

set(CMAKE_CXX_STANDARD 17)

add_executable(VulkanTriangle main.cpp)

set(GLFW_DIR "C:/Libraries/GLFW")
set(VULKAN_SDK_PATH "C:/VulkanSDK/1.3.290.0")

include_directories(${GLFW_DIR}/include)

include_directories(${VULKAN_SDK_PATH}/Include)


target_link_directories(${PROJECT_NAME} PUBLIC ${VULKAN_SDK_PATH}/Lib)
target_link_directories(${PROJECT_NAME} PUBLIC ${GLFW_DIR}/lib-mingw-w64)

target_link_libraries(${PROJECT_NAME} glfw3)
target_link_libraries(${PROJECT_NAME} vulkan-1)


set(SETUP_SCRIPT ${CMAKE_SOURCE_DIR}/setup.bat)


add_custom_target(run_setup
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
        COMMAND ${CMAKE_COMMAND} -E env cmd /c ${SETUP_SCRIPT}
        VERBATIM
)

add_dependencies(${PROJECT_NAME} run_setup)