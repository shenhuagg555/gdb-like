cmake_minimum_required(VERSION "3.25")
project(gdb-like C)

set(CMAKE_C_STANDARD 99)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}")

# Register Zydis dependency.
# Disable build of tools and examples.
option(ZYDIS_BUILD_TOOLS "" OFF)
option(ZYDIS_BUILD_EXAMPLES "" OFF)
add_subdirectory("deps/zydis")

# Add our project executable
add_executable(gdb-like ast.c cmdFuncs.c main.c)

add_compile_definitions("PACKAGE=gdb-like")
add_compile_definitions("PACKAGE_VERSION=1")

# Have CMake link our project executable against Zydis.
target_link_libraries("gdb-like" PRIVATE "Zydis" -lbfd -liberty -ldl -lz)
