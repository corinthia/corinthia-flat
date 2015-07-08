cmake_minimum_required(VERSION 3.1)
project(Flat)

message("Source directory is " ${CMAKE_SOURCE_DIR})
message("Build directory is " ${CMAKE_BINARY_DIR})

# Make sure we're not building in the root of the source tree
if ("${CMAKE_SOURCE_DIR}" STREQUAL "${CMAKE_BINARY_DIR}")
    message(FATAL_ERROR
    "
    Building in the source directory is not supported. Instead, you should
    create another directory specifically for the build. For example:
    
    mkdir ~/build/corinthia
    cd ~/build/corinthia
    cmake -G \"${CMAKE_GENERATOR}\" ${CMAKE_SOURCE_DIR}
    
    Before this will work, you should delete CMakeCache.txt and
    the CMakeFiles directory that were just generated in the source
    directory.")
endif()

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/bin)

set(LIBS )

if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    set(CMAKE_C_FLAGS "-std=c99 -D_GNU_SOURCE -g -fPIC")
endif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

if(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    set(CMAKE_C_FLAGS "/DWIN64 /D_WINDOWS /W3 /wd4090 /wd4996")
endif(${CMAKE_SYSTEM_NAME} MATCHES "Windows")

add_subdirectory(src)
