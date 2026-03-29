### 56.2 Mutable Lambdas

```cpp
int x = 10;
auto f = [x]() mutable { x++; return x; };
```