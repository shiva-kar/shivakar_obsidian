## 33. Memory Management Advanced & Undefined Behavior

- Undefined behavior sources: use-after-free, double-delete, data races
    
- Tools: sanitizers (`-fsanitize=address,undefined`), valgrind
    
- Best practices: prefer RAII and smart pointers