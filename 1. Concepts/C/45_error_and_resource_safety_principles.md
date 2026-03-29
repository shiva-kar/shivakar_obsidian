## 45. Error and Resource Safety Principles

- Use RAII and smart pointers.
    
- Prefer `std::vector` over dynamic arrays.
    
- Use exceptions for recoverable runtime errors.
    
- Use `assert()` for programmer errors and `static_assert()` for compile-time guarantees.
    
- Always ensure strong exception safety (operations either succeed fully or leave state unchanged).
    

---