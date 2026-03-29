### 56.4 Capture Move (C++14)

```cpp
auto ptr = std::make_unique<int>(42);
auto f = [p = std::move(ptr)] { return *p; };
```

---