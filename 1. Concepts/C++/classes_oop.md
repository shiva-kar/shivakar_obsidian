# classes OOP

## Core Idea
Consolidated concept from prior micro-notes.

## Legacy Notes (archived)

### 17 unions std variant 2

## 17. Unions & std::variant

- Unions exist but have restrictions
    
- Prefer `std::variant` (C++17) for type-safe discriminated unions

### 52 design patterns c implementation 2

## 52. Design Patterns (C++ Implementation)

### 71 1 raii resource acquisition is initialization

### 71.1 RAII (Resource Acquisition Is Initialization)

- Acquire resources in constructors, release in destructors.

### class raii example 2

### Class + RAII example

```cpp
#include <iostream>
#include <fstream>
#include <string>

class Logger {
    std::ofstream out;
public:
    Logger(const std::string &file): out(file) {}
    void log(const std::string &s) { out << s << '\n'; }
    // destructor closes ofstream automatically
};
```

