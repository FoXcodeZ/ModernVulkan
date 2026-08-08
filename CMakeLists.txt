cmake_minimum_required(VERSION 3.10)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

project(ModernVulkan LANGUAGES CXX)

find_package(Vulkan REQUIRED)
find_package(glfw3 3.4 REQUIRED)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


set(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(INC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/include")

file(GLOB ENGINE_SOURCES CONFIGURE_DEPENDS "${SRC_DIR}/*.cpp")
file(GLOB ENGINE_HEADERS CONFIGURE_DEPENDS "${INC_DIR}/*.hpp")

add_executable(ModernVulkan)

target_sources(ModernVulkan PRIVATE ${ENGINE_SOURCES})
target_include_directories(ModernVulkan PUBLIC "${INC_DIR}")

target_link_libraries(ModernVulkan PRIVATE glfw Vulkan::Vulkan)
