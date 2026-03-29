# Interoperability

# advanced topics

## Core Idea
Consolidated concept from prior micro-notes.

## Legacy Notes (archived)

### 22 modern c features c 11 c 14 c 17 c 20 2

## 22. Modern C++ Features (C++11, C++14, C++17, C++20)

- Move semantics: rvalue references `T&&`, `std::move`, `std::forward`
    
- Rule of Five: destructor, copy ctor, copy assignment, move ctor, move assignment
    
- `= default`, `= delete`
    
- Lambdas: `[capture](args){ body }` (C++11)
    
- `auto` for type deduction
    
- Structured bindings (C++17)
    
- `std::optional`, `std::variant`, `std::any` (C++17)
    
- Concepts (C++20) — optional advanced topic
    

Example lambda:

```cpp
auto sum = [](int a, int b){ return a + b; };
```

### 30 namespaces linkage 2

## 30. Namespaces & Linkage

- `namespace` for scope and preventing name collisions
    
- `inline namespace` and `anonymous namespace`
    
- `extern "C"` for C interop

### 36 networking sockets brief 2

## 36. Networking & Sockets (brief)

- C++ has no standard socket library; use Boost.Asio or OS APIs.
    
- Example: use `boost::asio` for cross-platform networking.

### 51 1 namespaces 2

### 51.1 Namespaces

- Group related declarations and avoid symbol collisions.
    

```cpp
namespace math {
    double square(double x) { return x * x; }
}
```

Access with `math::square(5)`.

### 51 2 nested namespaces 2

### 51.2 Nested Namespaces

```cpp
namespace graphics::shapes {
    class Circle {};
}
```

### 51 3 inline and anonymous namespaces 2

### 51.3 Inline and Anonymous Namespaces

- `inline namespace` allows versioning.
    
- `namespace { }` gives internal linkage (local to translation unit).

### 51 namespaces and modularization 2

## 51. Namespaces and Modularization

### 63 2 mixing c and c code 2

### 63.2 Mixing C and C++ Code

- C++ code can call C libraries by wrapping headers in:
    

```cpp
#ifdef __cplusplus
extern "C" {
#endif
// C declarations
#ifdef __cplusplus
}
#endif
```

---

### 63 interfacing c and c 2

## 63. Interfacing C and C++

### 65 testing in c 2

## 65. Testing in C++

### 67 1 runtime type information rtti

### 67.1 Runtime Type Information (RTTI)

- `typeid(obj)` returns type info.
    
- `dynamic_cast` for downcasting polymorphic types.

### 67 reflection and introspection c 20 proposals 2

## 67. Reflection and Introspection (C++20+ proposals)

### 68 1 standard and third party libraries 2

### 68.1 Standard and Third-Party Libraries

C++ has no official networking API until C++23. Common options:

- **Boost.Asio** (cross-platform, low-level)
    
- **cpp-httplib** (header-only HTTP)
    
- **cpr** (modern HTTP client wrapper)
    
- **Qt Network** (event-driven networking)

### 68 3 http client example cpr 2

### 68.3 HTTP Client Example (cpr)

```cpp
#include <cpr/cpr.h>
#include <iostream>

int main() {
    auto r = cpr::Get(cpr::Url{"https://example.com"});
    std::cout << r.status_code << "\n" << r.text;
}
```

---

### 68 networking in c 2

## 68. Networking in C++

### 69 gui development in c 2

## 69. GUI Development in C++

### 70 embedded systems with c 2

## 70. Embedded Systems with C++

### 71 c software architecture principles 2

## 71. C++ Software Architecture Principles

### 75 1 common frameworks 2

### 75.1 Common Frameworks

- **SFML**
    
- **SDL2**
    
- **Raylib**
    
- **Unreal Engine (C++)**

### lambda stl example 2

### Lambda + STL example

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{3,1,4,1,5};
    std::sort(v.begin(), v.end(), [](int a, int b){ return a < b; });
    for (int x : v) std::cout << x << ' ';
}
```

### o 2

## 2. Variables, Types & I/O

- Built-in types: `char, short, int, long, long long, float, double, bool, wchar_t`
    
- C++-specific: `std::string`, `std::nullptr_t`
    
- `auto` type deduction
    
- `constexpr`, `const`
    
- I/O: `std::cin`, `std::cout`, `std::cerr`, `std::getline`
    

```cpp
#include <iostream>
#include <string>

int main() {
    std::string name;
    std::cout << "Enter name: ";
    std::getline(std::cin, name);
    std::cout << "Hello, " << name << '\n';
}
```




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

