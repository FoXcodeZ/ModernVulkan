cmake_minimum_required(VERSION 3.10)

project(ModernVulkan LANGUAGES CXX)

find_package(Vulkan REQUIRED COMPONENTS volk shaderc_combined)
find_package(SDL3 REQUIRED)
find_package(glm REQUIRED)

set(CMAKE_CXX_STANDARD 26)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(INC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/include")

file(GLOB ENGINE_SOURCES CONFIGURE_DEPENDS "${SRC_DIR}/*.cpp")
file(GLOB ENGINE_HEADERS CONFIGURE_DEPENDS "${INC_DIR}/*.hpp")

add_executable(ModernVulkan)

if(MSVC)
    target_compile_options(ModernVulkan PRIVATE /std:c++latest)
endif()
target_sources(ModernVulkan PRIVATE ${ENGINE_SOURCES})

target_link_libraries(ModernVulkan PRIVATE
    Vulkan::Vulkan
    Vulkan::volk
    Vulkan::shaderc_combined
    SDL3::SDL3
    glm::glm
)
