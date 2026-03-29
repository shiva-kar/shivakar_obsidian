### 44.1 `constexpr` and `consteval`

```cpp
constexpr int sqr(int n) { return n * n; }
consteval int cube(int n) { return n * n * n; } // must run at compile time
```