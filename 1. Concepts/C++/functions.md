# functions

## Core Idea
Consolidated concept from prior micro-notes.

## Legacy Notes (archived)

### 21 inline constexpr consteval 2

## 21. Inline, constexpr, consteval

- `inline` functions and variables (C++17 inline variables)
    
- `constexpr` functions and variables (compile-time evaluation)
    
- `consteval` (C++20) forces compile-time evaluation

### 31 operator overloading 2

## 31. Operator Overloading

- Overload operators as member or non-member functions
    
- Common overloads: `operator+`, `operator=`, `operator<<` (stream insertion)
    
- Keep semantics intuitive
    

```cpp
#include <iostream>

struct Vec {
    int x,y;
    Vec(int a,int b):x(a),y(b){}
    Vec operator+(const Vec& o) const { return Vec(x+o.x,y+o.y); }
};

std::ostream& operator<<(std::ostream& os, const Vec& v) {
    return os << '(' << v.x << ',' << v.y << ')';
}
```

### 53 1 template argument deduction 2

### 53.1 Template Argument Deduction

- Compiler deduces template parameters automatically:
    

```cpp
template<typename T>
void f(T x) { }
f(42); // deduces T = int
```

### 53 2 trailing return type 2

### 53.2 Trailing Return Type

```cpp
template<typename T, typename U>
auto add(T a, U b) -> decltype(a + b) { return a + b; }
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

