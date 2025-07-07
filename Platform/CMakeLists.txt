cmake_minimum_required(VERSION 3.8)

add_library(adiosy_platform STATIC
    Private/AdLog.cpp
    Private/AdWindow.cpp
    Private/Window/AdGLFWwindow.cpp

    Private/AdGraphicContext.cpp
    Private/Graphic/AdVKGraphicContext.cpp
)

target_include_directories(adiosy_platform PUBLIC External)

# glfw
add_subdirectory(External/glfw)
target_link_libraries(adiosy_platform PRIVATE glfw)

# Vulkan
find_package(Vulkan REQUIRED)
if(Vulkan_FOUND)
    message("----> Find vulkan success: ${Vulkan_INCLUDE_DIRS}")
endif()
target_include_directories(adiosy_platform PRIVATE ${Vulkan_INCLUDE_DIRS})
target_link_libraries(adiosy_platform PRIVATE ${Vulkan_LIBRARY})