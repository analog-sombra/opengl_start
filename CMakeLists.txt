# ============================================================================
# OpenGL Project with GLFW, GLAD, and fmt - CMake Configuration
# ============================================================================
# This is the root CMakeLists.txt file for an OpenGL project using modern C++23
# Dependencies are managed through vcpkg package manager
# 
# Required packages (installed via vcpkg):
# - fmt: Modern formatting library for C++
# - glfw3: Cross-platform library for OpenGL, OpenGL ES, and Vulkan
# - glad: OpenGL function loader library
# ============================================================================

# Specify minimum CMake version (3.28 required for C++23 module support)
cmake_minimum_required(VERSION 3.28)

# ============================================================================
# vcpkg Integration Setup
# ============================================================================
# Set vcpkg toolchain file if not already defined
# This tells CMake to use vcpkg for package management
# The VCPKG_ROOT environment variable should point to your vcpkg installation
if(NOT DEFINED CMAKE_TOOLCHAIN_FILE)
    set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake" CACHE STRING "Vcpkg toolchain file")
endif()

# ============================================================================
# Project Configuration
# ============================================================================
# Define project name, version, and programming language
# The project name will also be used as the executable name
project(Rocket VERSION 1.0.0 LANGUAGES CXX)

# ============================================================================
# C++ Standard and Compiler Settings
# ============================================================================
# Require C++23 - This is a hard requirement for the project
set(CXX_STANDARD_REQUIRED ON)      # Make C++23 compliance mandatory
set(CMAKE_CXX_STANDARD 23)         # Set default C++ standard for all targets
set(CMAKE_CXX_SCAN_FOR_MODULES ON) # Enable C++20/23 module scanning (if using modules)

# ============================================================================
# Source Files Configuration
# ============================================================================
# List all source files for the project
# Organized in src/ directory with headers in src/header/
set(SOURCES 
    src/main.cpp
    src/shaderClass.cpp
    src/VAO.cpp
    src/VBO.cpp
    src/EBO.cpp
)

# Include directories for header files
include_directories(${CMAKE_SOURCE_DIR}/src/header)

# ============================================================================
# Package Dependencies
# ============================================================================
# Find and configure required external libraries managed by vcpkg

# fmt: Modern C++ formatting library (alternative to printf/iostream)
# Provides fast, safe, and expressive string formatting
find_package(fmt CONFIG REQUIRED)

# GLFW3: Cross-platform library for creating windows and handling input
# Essential for OpenGL context creation and window management
find_package(glfw3 CONFIG REQUIRED)

# GLAD: OpenGL function loader library
# Loads OpenGL function pointers at runtime for the current platform
find_package(glad CONFIG REQUIRED)

# ============================================================================
# Executable Target Configuration
# ============================================================================
# Create the main executable target using the project name
# This will create an executable named "Rocket.exe" (on Windows)
add_executable(${PROJECT_NAME} ${SOURCES})

# ============================================================================
# Library Linking Configuration
# ============================================================================
# Link the required libraries to our executable
# PRIVATE means these libraries are only needed for building this target,
# not for any targets that might depend on this one
target_link_libraries(${PROJECT_NAME}
    PRIVATE 
    fmt::fmt        # Modern C++ formatting library
    glfw           # Window creation and input handling
    glad::glad     # OpenGL function loader
)

# ============================================================================
# Optional: Additional Compiler Flags and Build Settings
# ============================================================================
# Uncomment and modify these sections as needed for your project

# Set additional compiler-specific flags for better debugging/optimization
# target_compile_options(${PROJECT_NAME} PRIVATE
#     $<$<CXX_COMPILER_ID:MSVC>:/W4>           # MSVC: Enable level 4 warnings
#     $<$<CXX_COMPILER_ID:GNU>:-Wall -Wextra>  # GCC: Enable common warnings
#     $<$<CXX_COMPILER_ID:Clang>:-Wall -Wextra> # Clang: Enable common warnings
# )

# Set build type specific compiler flags
# target_compile_options(${PROJECT_NAME} PRIVATE
#     $<$<CONFIG:Debug>:-DDEBUG_BUILD>         # Define DEBUG_BUILD for debug builds
#     $<$<CONFIG:Release>:-DNDEBUG -O3>        # Optimize for release builds
# )

# ============================================================================
# Post-Build: Copy Shader Files
# ============================================================================
# Copy shader files to the build directory so the executable can find them
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_SOURCE_DIR}/src/shader
        $<TARGET_FILE_DIR:${PROJECT_NAME}>
    COMMENT "Copying shader files to build directory"
)

# ============================================================================
# Build Instructions for Developers
# ============================================================================
# To build this project:
# 1. Make sure vcpkg is installed and VCPKG_ROOT environment variable is set
# 2. Install dependencies: vcpkg install fmt glfw3 glad
# 3. Configure: cmake -S . -B build -G "Visual Studio 17 2022" -A x64
# 4. Build: cmake --build build --config Debug
# 5. Run: ./build/Debug/Rocket.exe (on Windows)
# ============================================================================