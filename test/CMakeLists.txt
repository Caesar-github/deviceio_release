cmake_minimum_required(VERSION 2.8.0 FATAL_ERROR)

set(SRC_FILES
    DeviceIOTest.cpp
    bt_test.cpp
    rk_ble_app.c
)

if(CPU_ARCH STREQUAL "arm")
    link_directories("${CMAKE_CURRENT_SOURCE_DIR}/../DeviceIO/lib32")
endif()

if(CPU_ARCH STREQUAL "aarch64")
    link_directories("${CMAKE_CURRENT_SOURCE_DIR}/../DeviceIO/lib64")
endif()

add_executable(deviceio_test ${SRC_FILES})
target_include_directories(deviceio_test PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/../DeviceIO/include" )
target_link_libraries(deviceio_test pthread DeviceIo asound)

install(TARGETS deviceio_test DESTINATION bin)
