cmake_minimum_required(VERSION 3.10)

project(gpio)

# Set the C standard
set(CMAKE_C_STANDARD 99)


include_directories(${DESTDIR}${PREFIX}/include)

set(SRC gpio.c readall.c)

add_executable(gpio ${SRC})

# Set the compilation flags
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O2 -Wall -Wextra -Winline -pipe")

# Set the linker flags and libraries
target_link_libraries(gpio wiringPi devLib pthread rt m crypt)

# Custom commands for installation
install(TARGETS gpio DESTINATION ${DESTDIR}${PREFIX}/bin)