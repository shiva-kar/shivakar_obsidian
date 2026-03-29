### 76.2 Secure Coding Guidelines

- Use bounds-checked containers.
    
- Validate all input.
    
- Prefer RAII for resource control.
    
- Avoid `strcpy`, `sprintf` — use `std::snprintf`, `std::string`.