## 29. Variadic Templates & Parameter Packs

- Implement `printf`-like functionality with type safety using variadic templates
    
- Example skeleton:
    

```cpp
template<typename... Args>
void log(Args&&... args) {
    (std::cout << ... << args) << '\n'; // fold expression (C++17)
}
```