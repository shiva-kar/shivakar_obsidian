## 19. Error Handling

- Exceptions: `try`, `catch`, `throw`
    
- Prefer typed exceptions; avoid using exceptions for control-flow in performance-critical code
    
- `std::error_code` / `std::expected` (proposal/3rd-party libs) for alternate patterns
    
- `noexcept` for functions that must not throw
    

```cpp
try {
    throw std::runtime_error("error");
} catch (const std::exception &e) {
    std::cerr << e.what() << '\n';
}
```