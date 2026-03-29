### 42.1 Template Specialization

```cpp
template<typename T>
void printType() { std::cout << "Generic type\n"; }

template<>
void printType<int>() { std::cout << "int type\n"; }
```