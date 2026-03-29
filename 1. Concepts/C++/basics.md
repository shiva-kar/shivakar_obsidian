# basics

## Core Idea
Consolidated concept from prior micro-notes.

## Legacy Notes (archived)

### 1 1 basic program structure 2

## 1.1 Basic Program Structure

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World\n";
    return 0;
}
```

- File extension `.cpp`
    
- `main()` signature variations: `int main()`, `int main(int argc, char** argv)`

### 1 5 compiling running 2

### 1.2 Showing Output / 1.3 Importance of main / 1.4 Comments / 1.5 Compiling & Running

- compile: `g++ -std=c++17 main.cpp -o main`
    
- run: `./main` (Unix) or `main.exe` (Windows)
    
- single-line `//`, multi-line `/* ... */`

### 1 first c program 2

## 1. First C++ Program

### 8 storage duration type modifiers 2

## 8. Storage Duration & Type Modifiers

- `static`, `extern`, `thread_local`
    
- `signed`/`unsigned`, `short`/`long`
    
- `mutable` (for `const` object member mutation)
    
- Storage classes and linkage differences in C++

### hello world 2

### Hello World

```cpp
#include <iostream>
int main(){ std::cout << "Hello, World\n"; }
```

### installation compiler setup 2

### Installation & Compiler Setup

- What is an IDE
    
- Need for an IDE
    
- Windows installation (MSYS2 + MinGW-w64 or Visual Studio)
    
- macOS installation (Xcode + clang)
    
- Linux installation (g++, clang)
    
- Installing VS Code extensions (C/C++, CMake Tools)
    
- Compiler quick checks: `g++ --version`, `clang++ --version`
    
- Build systems: `g++` CLI, CMake example (basic `CMakeLists.txt`)

### mac installation

### Mac Installation
- Search VS Code on Google
- Download and install Visual Studio Code
- Install C/C++ extensions
- Ensure Clang is installed (comes with Xcode)
- Verify installation using `clang --version`
Looking at the basic topics covered, here are some important fundamental C programming topics that were missed or could use more detailed coverage:

### windows installation

### Windows Installation
- Search VS Code on Google
- Download and install Visual Studio Code
- Install C/C++ extensions
- Download and install MSYS2
- Install MinGW toolchain
- Add MinGW to system PATH
- Configure VS Code for C/C++ development



## Why it exists
Real engineering problem this concept solves.


## Code Pattern
```c
// minimal reusable example
```


## Common Mistakes
- Misapplying the concept without constraints.
- Ignoring edge cases and failure paths.


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?


## Related
- [[templates]]
- [[stl]]
- [[memory_management]]

