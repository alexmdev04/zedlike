cmake_minimum_required(VERSION 3.28)
project(zedlike C)
set(CMAKE_C_STANDARD 23)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # Generates compile_commands.json

include(FetchContent)
FetchContent_Declare(
        raylib
        DOWNLOAD_EXTRACT_TIMESTAMP OFF
        URL https://github.com/raysan5/raylib/archive/refs/tags/5.5.tar.gz
        FIND_PACKAGE_ARGS
)
FetchContent_MakeAvailable(raylib)

find_package(raylib 3.0 REQUIRED) # Requires at least version 3.0

add_executable(${PROJECT_NAME} main.c)

target_link_libraries(${PROJECT_NAME} raylib)

# Checks if OSX and links appropriate frameworks (only required on MacOS)
if (APPLE)
    target_link_libraries(${PROJECT_NAME} "-framework IOKit")
    target_link_libraries(${PROJECT_NAME} "-framework Cocoa")
    target_link_libraries(${PROJECT_NAME} "-framework OpenGL")
endif()