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