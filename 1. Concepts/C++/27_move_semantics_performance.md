## 27. Move Semantics & Performance

- Move constructors and move assignment for efficient transfers
    
- `std::move` marks rvalue. Use `std::move` when you want to transfer resources.
    
- Avoid unnecessary copies: use `const T&` or `T&&` appropriately.