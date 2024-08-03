cmake_minimum_required(VERSION 3.10)

project(devLib)

include_directories(.)

file(GLOB SRC "*.c")
add_library(devLib ${SRC})

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O2 -Wall -Wextra -Winline -pipe")

# Set the linker flags and libraries
target_link_libraries(devLib wiringPi rt m crypt)

target_include_directories(devLib
    INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:include>
)
