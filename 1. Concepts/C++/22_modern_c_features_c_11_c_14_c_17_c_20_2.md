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