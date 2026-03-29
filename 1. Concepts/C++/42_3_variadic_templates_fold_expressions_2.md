### 42.3 Variadic Templates & Fold Expressions

```cpp
template<typename... Args>
void printAll(Args&&... args) {
    (std::cout << ... << args) << '\n';
}
```

---