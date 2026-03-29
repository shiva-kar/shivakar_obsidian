## 34. Build Systems & Tooling

- `g++` flags (`-std=c++17`, `-O2`, `-g`, `-Wall`, `-Wextra`)
    
- CMake example:
    

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyApp CXX)
set(CMAKE_CXX_STANDARD 17)
add_executable(myapp main.cpp)
```

- Use clang-tidy, clang-format for style and static analysis