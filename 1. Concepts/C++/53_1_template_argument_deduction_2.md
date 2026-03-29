### 53.1 Template Argument Deduction

- Compiler deduces template parameters automatically:
    

```cpp
template<typename T>
void f(T x) { }
f(42); // deduces T = int
```