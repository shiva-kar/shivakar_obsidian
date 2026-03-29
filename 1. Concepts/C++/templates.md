# templates

## Core Idea
Consolidated concept from prior micro-notes.

## Legacy Notes (archived)

### 20 templates functions classes 2

## 20. Templates (Functions & Classes)

- Function templates
    
- Class templates
    
- Template specialization and partial specialization
    
- Variadic templates (C++11)
    
- `typename` vs `class` keyword usage in templates
    
- Example:
    

```cpp
template<typename T>
T add(T a, T b) { return a + b; }

template<typename T>
class Box {
public:
    Box(T v): val(v) {}
    T get() const { return val; }
private:
    T val;
};
```

### 28 templates advanced sfinae traits and concepts

## 28. Templates Advanced: SFINAE, Traits, and Concepts

- SFINAE (Substitution Failure Is Not An Error)
    
- `std::enable_if`, `std::is_same`, `std::decay`, type traits
    
- C++20 Concepts to write clearer constraints

### 42 1 template specialization 2

### 42.1 Template Specialization

```cpp
template<typename T>
void printType() { std::cout << "Generic type\n"; }

template<>
void printType<int>() { std::cout << "int type\n"; }
```

### 42 2 partial specialization 2

### 42.2 Partial Specialization

```cpp
template<typename T, typename U>
struct Pair { };

template<typename T>
struct Pair<T, T> { }; // specialized when both same type
```

### 42 3 variadic templates fold expressions 2

### 42.3 Variadic Templates & Fold Expressions

```cpp
template<typename... Args>
void printAll(Args&&... args) {
    (std::cout << ... << args) << '\n';
}
```

---

### 42 advanced templates 2

## 42. Advanced Templates

### template function 2

### Template function

```cpp
#include <iostream>

template<typename T>
T add(T a, T b) { return a + b; }

int main() {
    std::cout << add<int>(2,3) << '\n';
}
```

