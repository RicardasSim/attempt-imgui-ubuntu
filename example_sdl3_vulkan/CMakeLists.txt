# Example usage:
#  mkdir build
#  cd build
#  cmake ..

cmake_minimum_required(VERSION 2.8)
project(imgui_example_sdl3_vulkan C CXX)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug CACHE STRING "" FORCE)
endif()

set(CMAKE_CXX_STANDARD 11)
set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DVK_PROTOTYPES")
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DVK_PROTOTYPES")

# SDL3 (local)
set(SDL3_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/include")
include_directories(${SDL3_INCLUDE_DIR})

# Dear ImGui
set(IMGUI_DIR ../imgui)
include_directories(${IMGUI_DIR} ${IMGUI_DIR}/backends ..)

# Specify the path to the shared library
set(LIBRARY_PATH "${CMAKE_SOURCE_DIR}/lib")
link_directories(${LIBRARY_PATH})
set(SDL3_SHARED_LIB "SDL3")

# Libraries
find_package(Vulkan REQUIRED)
set(VULKAN_LIB "Vulkan::Vulkan")

file(GLOB sources *.cpp)

add_executable(example_sdl3_vulkan ${sources} ${IMGUI_DIR}/backends/imgui_impl_sdl3.cpp ${IMGUI_DIR}/backends/imgui_impl_vulkan.cpp ${IMGUI_DIR}/imgui.cpp ${IMGUI_DIR}/imgui_draw.cpp ${IMGUI_DIR}/imgui_demo.cpp ${IMGUI_DIR}/imgui_tables.cpp ${IMGUI_DIR}/imgui_widgets.cpp)
target_link_libraries(example_sdl3_vulkan ${SDL3_SHARED_LIB} ${VULKAN_LIB})

