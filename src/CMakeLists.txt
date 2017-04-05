cmake_minimum_required(VERSION 2.6)

project(pokerstove)

enable_testing()

# check_function_exists does not work for builtins, so use try_compile.
try_compile(HAVE_BUILTIN_BITOPS
            "${PROJECT_BINARY_DIR}"
            "${PROJECT_SOURCE_DIR}/TestBuiltinBitops.cpp")

# Set up the configure file.
configure_file("${PROJECT_SOURCE_DIR}/Config.h.in"
               "${PROJECT_BINARY_DIR}/Config.h")

# Also search for includes in PROJECT_BINARY_DIR to find config.h.
include_directories(lib/ ext/ "${PROJECT_BINARY_DIR}")
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
add_subdirectory(lib/pokerstove/peval)
add_subdirectory(lib/pokerstove/penum)
add_subdirectory(lib/pokerstove/util)
