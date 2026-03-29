# file io

## Core Idea
Consolidated concept from prior micro-notes.

## Legacy Notes (archived)

### 34 build systems tooling 2

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

### 72 1 text based json xml 2

### 72.1 Text-Based (JSON, XML)

- Libraries: nlohmann/json, rapidjson, pugixml
    

```cpp
#include <nlohmann/json.hpp>
#include <iostream>
using json = nlohmann::json;

int main() {
    json j = { {"name", "Alice"}, {"age", 25} };
    std::cout << j.dump(4);
}
```

### 72 2 binary serialization 2

### 72.2 Binary Serialization

- Use `<fstream>` or libraries like cereal, protobuf.
    

```cpp
#include <cereal/archives/binary.hpp>
#include <fstream>

struct Data { int x; template<class Ar> void serialize(Ar& ar){ ar(x); } };
```

---

### 73 1 simple logging 2

### 73.1 Simple Logging

```cpp
#include <iostream>
#define LOG(x) std::cout << __FILE__ << ":" << __LINE__ << " " << x << "\n"
```

### 79 2 precompiled headers 2

### 79.2 Precompiled Headers

```bash
g++ -std=c++20 -x c++-header common.hpp -o common.hpp.gch
```

