### 51.1 Namespaces

- Group related declarations and avoid symbol collisions.
    

```cpp
namespace math {
    double square(double x) { return x * x; }
}
```

Access with `math::square(5)`.