cmake_minimum_required(VERSION 3.10)

project(wiringPi)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# Set the source files
set(SRC
    wiringPi.c
    wiringSerial.c wiringShift.c
    piHiPri.c piThread.c
    wiringPiSPI.c wiringPiI2C.c
    softPwm.c softTone.c
    mcp23008.c mcp23016.c mcp23017.c
    mcp23s08.c mcp23s17.c
    sr595.c
    pcf8574.c pcf8591.c
    mcp3002.c mcp3004.c mcp4802.c mcp3422.c
    max31855.c max5322.c ads1115.c
    sn3218.c
    bmp180.c htu21d.c ds18b20.c rht03.c
    drcSerial.c drcNet.c
    pseudoPins.c
    wpiExtensions.c
    w25q64.c
    oled.c
)

set(STATIC libwiringPi.a)
set(DYNAMIC libwiringPi.so.${VERSION})

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O2 -D_GNU_SOURCE -Wformat=2 -Wextra -Winline -pipe -fPIC")

add_library(wiringPi SHARED ${SRC})
target_link_libraries(wiringPi m pthread rt crypt)
# set_target_properties(wiringPi PROPERTIES VERSION ${VERSION} SOVERSION 1)

install(TARGETS wiringPi DESTINATION ${DESTDIR}${PREFIX}/lib)
# install(FILES ${HEADERS} DESTINATION ${DESTDIR}${PREFIX}/include)
install(CODE "execute_process(COMMAND ${CMAKE_COMMAND} -E create_symlink libwiringPi.so.${VERSION} libwiringPi.so)")

target_include_directories(wiringPi
    INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:include>
)
