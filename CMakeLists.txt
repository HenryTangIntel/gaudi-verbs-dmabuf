cmake_minimum_required(VERSION 3.10)
project(RDMADmabuf LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Ensure POSIX functions are available
add_definitions(-D_POSIX_C_SOURCE=200809L)

# Find required packages
find_package(PkgConfig REQUIRED)
pkg_check_modules(IBVERBS REQUIRED libibverbs)

# Include directories
include_directories(
    ${IBVERBS_INCLUDE_DIRS}
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    /opt/habanalabs/src/hl-thunk/include
    /opt/habanalabs/src/hl-thunk/include/uapi
    /opt/habanalabs/src/hl-thunk/src
    /opt/habanalabs/src/habanalabs/include/uapi
    /opt/habanalabs/src/hldk/include/specs/misc
    /opt/habanalabs/src/hl-thunk/include/specs/common
    /usr/include
    /usr/include/drm
)

# Link directories
link_directories(
    ${IBVERBS_LIBRARY_DIRS}
    /opt/habanalabs/src/hl-thunk/build/lib
    /usr/lib/x86_64-linux-gnu
)

# Glob hlthunk libraries
file(GLOB HLTHUNK_LIBRARIES "/opt/habanalabs/src/hl-thunk/build/lib/*.so" "/opt/habanalabs/src/hl-thunk/build/lib/*.a")

# Source files
set(SOURCES
    src/hpuverbs.cpp
)

# Server executable
add_executable(server
    server.cpp
    ${SOURCES}
)

target_link_libraries(server
    PRIVATE
    ${IBVERBS_LIBRARIES}
    ${HLTHUNK_LIBRARIES}
)

# Client executable
add_executable(client
    client.cpp
    ${SOURCES}
)

target_link_libraries(client
    PRIVATE
    ${IBVERBS_LIBRARIES}
    ${HLTHUNK_LIBRARIES}
)

# Installation
install(TARGETS server client
    DESTINATION bin
)
