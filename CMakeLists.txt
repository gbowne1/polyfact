cmake_minimum_required(VERSION 3.13)

# Set project metadata
project(libpolyfact
    VERSION 1.0.0
    DESCRIPTION "C++ Library for polynomial factorization"
    HOMEPAGE_URL "https://example.com/libpolyfact"
    LANGUAGES CXX
)

# Enable testing
include(CTest)
enable_testing()

# Additional variables
set(AUTHOR "Gregory Bowne")
set(LICENSE "MIT")

# Check for gcc
find_program(GCC_COMPILER gcc)
if(GCC_COMPILER)
    set(CMAKE_C_COMPILER ${GCC_COMPILER})
endif()

# Check for g++
find_program(GPP_COMPILER g++)
if(GPP_COMPILER)
    set(CMAKE_CXX_COMPILER ${GPP_COMPILER})
endif()

# Check for clang
find_program(CLANG_COMPILER clang)
if(CLANG_COMPILER)
    set(CMAKE_C_COMPILER ${CLANG_COMPILER})
    set(CMAKE_CXX_COMPILER ${CLANG_COMPILER}++)
endif()

# Check for cc and c++
find_program(CC_COMPILER cc)
if(CC_COMPILER)
    set(CMAKE_C_COMPILER ${CC_COMPILER})
endif()

find_program(CPP_COMPILER c++)
if(CPP_COMPILER)
    set(CMAKE_CXX_COMPILER ${CPP_COMPILER})
endif()

# Set compiler and architecture options
set(CMAKE_SYSTEM_PROCESSOR "x86")
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "-O3 -Wall -Werror -Wextra -pedantic")

# Set the build types
set(CMAKE_CONFIGURATION_TYPES "Debug;Release" CACHE STRING "Build configurations" FORCE)

# Set the build type if not already specified
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Build type" FORCE)
endif()

# Define the output directories for debug and release builds
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/build/debug)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/build/release)

# Add your source files to a variable
set(SOURCE_FILES
    src/greatest_common_factor.cpp
    src/grouping_method.cpp
    src/difference_of_squares.cpp
    # Add other source files here
)

# Create the library (shared or static)
add_library(polyfact SHARED ${SOURCE_FILES})  # For shared library
# add_library(polyfact STATIC ${SOURCE_FILES})  # For static library

# Include directories, additional configurations, etc.
target_include_directories(polyfact PUBLIC include)

# Add tests using ADD_TEST()
add_test(NAME TestGreatestCommonFactor COMMAND TestGreatestCommonFactor)
add_test(NAME TestGroupingMethod COMMAND TestGroupingMethod)
add_test(NAME TestDifferenceOfSquares COMMAND TestDifferenceOfSquares)