### 63.2 Mixing C and C++ Code

- C++ code can call C libraries by wrapping headers in:
    

```cpp
#ifdef __cplusplus
extern "C" {
#endif
// C declarations
#ifdef __cplusplus
}
#endif
```

---