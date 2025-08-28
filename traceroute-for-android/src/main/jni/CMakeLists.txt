cmake_minimum_required(VERSION 3.22.1)

project("traceroute")

# Set C standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Set Android platform and 16KB page size support
set(CMAKE_ANDROID_PLATFORM "latest")
set(CMAKE_ANDROID_SUPPORT_FLEXIBLE_PAGE_SIZES ON)

# Find all source files
file(GLOB_RECURSE LIBSUPP_SOURCES
        "${CMAKE_CURRENT_SOURCE_DIR}/libsupp/*.c"
)

file(GLOB_RECURSE TRACEROUTE_SOURCES
        "${CMAKE_CURRENT_SOURCE_DIR}/traceroute/*.c"
)

# Create the shared library
add_library(${CMAKE_PROJECT_NAME} SHARED
    ${LIBSUPP_SOURCES}
    ${TRACEROUTE_SOURCES}
)

# Include directories
target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/libsupp
    ${CMAKE_CURRENT_SOURCE_DIR}/traceroute
)

# Compiler flags - only PIC needed for shared libraries
target_compile_options(${CMAKE_PROJECT_NAME} PRIVATE
    -fPIC
)

# Link libraries
target_link_libraries(${CMAKE_PROJECT_NAME}
    android
    log
)