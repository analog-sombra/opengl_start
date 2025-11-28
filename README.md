# Rocket - OpenGL Project

A modern C++23 OpenGL project template using GLFW, GLAD, and fmt libraries for cross-platform graphics development.

## 📋 Project Overview

This project provides a solid foundation for OpenGL applications with:
- **Modern C++23** standard compliance
- **Cross-platform** support (Windows, macOS, Linux)
- **vcpkg** for dependency management
- **CMake** for build configuration
- **MSVC** compiler support (Visual Studio 2022)

## 🛠️ Dependencies

### Core Libraries
- **[fmt](https://fmt.dev/)** - Modern C++ formatting library
  - Fast, safe, and expressive string formatting
  - Alternative to printf/iostream for better performance
  
- **[GLFW3](https://www.glfw.org/)** - Cross-platform windowing library
  - Window creation and management
  - Input handling (keyboard, mouse, joystick)
  - OpenGL context creation
  
- **[GLAD](https://glad.dav1d.de/)** - OpenGL function loader
  - Loads OpenGL function pointers at runtime
  - Supports multiple OpenGL versions and extensions

### Build Tools
- **CMake 3.28+** - Build system generator
- **vcpkg** - Package manager for C++ libraries
- **Visual Studio 2022** - Compiler and IDE support

## 🚀 Getting Started

### Prerequisites

1. **Install Visual Studio 2022** with C++ development tools
2. **Install vcpkg**:
   ```powershell
   git clone https://github.com/Microsoft/vcpkg.git
   cd vcpkg
   .\bootstrap-vcpkg.bat
   ```
3. **Set environment variable**:
   ```powershell
   $env:VCPKG_ROOT = "C:\path\to\vcpkg"
   ```

### Building the Project

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd rocket
   ```

2. **Configure with CMake**:
   ```bash
   cmake -S . -B build
   ```
   This will automatically:
   - Download and install dependencies via vcpkg
   - Generate build files for your platform

3. **Build the project**:
   ```bash
   cmake --build build
   ```

4. **Run the executable**:
   ```bash
   # Windows
   .\build\Debug\Rocket.exe
   
   # Linux/macOS
   ./build/Debug/Rocket
   ```

## 📁 Project Structure

```
rocket/
├── CMakeLists.txt          # Main build configuration
├── vcpkg.json              # Dependency manifest
├── main.cpp                # Application entry point
├── README.md               # This file
└── build/                  # Build output directory
    └── Debug/
        └── Rocket.exe      # Compiled executable
```

## ⚙️ Configuration Details

### CMakeLists.txt Features
- **Automatic vcpkg integration** - No manual package installation required
- **C++23 standard enforcement** - Modern C++ features enabled
- **Cross-compiler support** - Works with MSVC, GCC, and Clang
- **Modular structure** - Easy to extend with additional source files

### vcpkg.json Manifest
- **Declarative dependencies** - All required packages listed explicitly
- **Version pinning** - Ensures consistent builds across environments
- **Automatic installation** - Dependencies installed during CMake configure

## 🔧 Development Workflow

### Adding New Source Files
1. Create your `.cpp` and `.h` files
2. Add them to the `SOURCES` list in `CMakeLists.txt`:
   ```cmake
   set(SOURCES 
       main.cpp
       src/renderer.cpp      # Add new files here
       src/window.cpp
   )
   ```

### Adding New Dependencies
1. Add to `vcpkg.json`:
   ```json
   "dependencies": [
     "fmt",
     "glfw3",
     "glad",
     "your-new-library"     // Add here
   ]
   ```
2. Add `find_package()` and linking in `CMakeLists.txt`

### Build Types
- **Debug** (default): Optimized for debugging with symbols
- **Release**: Optimized for performance
- **RelWithDebInfo**: Release with debug information

```bash
# Build release version
cmake --build build --config Release
```

## 🎯 Next Steps

This template provides the foundation for:
- **3D Graphics Applications** - OpenGL rendering pipelines
- **Game Development** - Real-time graphics and input handling
- **Visualization Tools** - Scientific or data visualization
- **Graphics Learning** - OpenGL tutorials and experiments

## 🐛 Troubleshooting

### Common Issues

1. **vcpkg not found**: Ensure `VCPKG_ROOT` environment variable is set
2. **CMake version too old**: Update to CMake 3.28 or newer
3. **Compiler not found**: Install Visual Studio 2022 with C++ tools
4. **Build fails**: Clean build directory and reconfigure

### Getting Help
- Check the CMake output for specific error messages
- Ensure all prerequisites are installed correctly
- Verify environment variables are set properly

## 📝 License

This project template is provided as-is for educational and development purposes.