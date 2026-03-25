cmake_minimum_required(VERSION 3.16)
project(displayxr-demos LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_STANDARD 11)

# Extension headers
include_directories(${CMAKE_SOURCE_DIR}/include)

# Common utilities
add_subdirectory(common)

# Demos
if(WIN32)
    add_subdirectory(gaussian_splatting/windows)
    add_subdirectory(spatial_os/windows)
elseif(APPLE)
    add_subdirectory(gaussian_splatting/macos)
endif()
