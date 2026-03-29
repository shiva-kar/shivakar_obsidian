### 53.2 Trailing Return Type

```cpp
template<typename T, typename U>
auto add(T a, U b) -> decltype(a + b) { return a + b; }
```