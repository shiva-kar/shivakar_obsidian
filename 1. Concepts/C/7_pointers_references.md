## 7. Pointers & References

- Raw pointers: declaration, `new`/`delete` (prefer smart pointers)
    
- Pointer to pointer
    
- References: `int &r = x;` (cannot be null, must be initialized)
    
- `nullptr` vs `NULL`
    
- `std::addressof`, `std::exchange` basics
    

```cpp
int x = 10;
int *p = &x;
int &r = x;
```