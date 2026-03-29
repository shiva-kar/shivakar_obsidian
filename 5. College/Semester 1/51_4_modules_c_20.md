### 51.4 Modules (C++20)

- Replace headers and preprocessor with compiled interfaces.
    

```cpp
export module math;
export int add(int a, int b) { return a + b; }
```

---