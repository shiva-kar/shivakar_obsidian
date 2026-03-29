### 42.2 Partial Specialization

```cpp
template<typename T, typename U>
struct Pair { };

template<typename T>
struct Pair<T, T> { }; // specialized when both same type
```