## 48. Coding Best Practices

1. Avoid raw pointers for ownership.
    
2. Prefer `std::vector` or `std::array` over raw arrays.
    
3. Pass large objects by reference.
    
4. Minimize `using namespace std;`
    
5. Use `enum class` instead of `#define` constants.
    
6. Prefer modern features (`auto`, range-for, RAII).
    
7. Always initialize variables.
    
8. Use consistent naming conventions.
    
9. Use tools: `clang-tidy`, `cppcheck`, `clang-format`.
    

---