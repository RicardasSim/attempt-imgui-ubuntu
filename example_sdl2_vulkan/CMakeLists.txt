# Example usage:
#  mkdir build
#  cd build
#  cmake ..

cmake_minimum_required(VERSION 2.8)
project(imgui_example_sdl2_vulkan C CXX)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug CACHE STRING "" FORCE)
endif()

set(CMAKE_CXX_STANDARD 11)
set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DVK_PROTOTYPES")
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DVK_PROTOTYPES")

# SDL2
find_package(SDL2 REQUIRED)
include_directories(imgui_example_sdl2_vulkan ${SDL2_INCLUDE_DIRS})

# Dear ImGui
set(IMGUI_DIR ../imgui)
include_directories(${IMGUI_DIR} ${IMGUI_DIR}/backends ..)

# Libraries
find_package(Vulkan REQUIRED)
set(LIBRARIES ${SDL2_LIBRARIES} "Vulkan::Vulkan")

file(GLOB sources *.cpp)

add_executable(example_sdl2_vulkan ${sources} ${IMGUI_DIR}/backends/imgui_impl_sdl2.cpp ${IMGUI_DIR}/backends/imgui_impl_vulkan.cpp ${IMGUI_DIR}/imgui.cpp ${IMGUI_DIR}/imgui_draw.cpp ${IMGUI_DIR}/imgui_demo.cpp ${IMGUI_DIR}/imgui_tables.cpp ${IMGUI_DIR}/imgui_widgets.cpp)
target_link_libraries(example_sdl2_vulkan ${LIBRARIES})

