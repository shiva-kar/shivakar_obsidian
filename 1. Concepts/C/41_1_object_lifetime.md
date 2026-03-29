### 41.1 Object Lifetime

- Automatic: stack allocation, destroyed when scope ends.
    
- Dynamic: created via `new`/`delete`, managed manually.
    
- RAII and smart pointers ensure deterministic cleanup.