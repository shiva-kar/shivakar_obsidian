## 23. Smart Pointers (detailed)

- `std::unique_ptr<T>`: sole ownership, lightweight
    
- `std::shared_ptr<T>`: reference-counted
    
- `std::weak_ptr<T>`: observe `shared_ptr` without ownership
    
- Use `unique_ptr` when ownership is unique. Use `shared_ptr` when shared ownership required.
    

```cpp
#include <memory>
struct Node { int val; std::unique_ptr<Node> next; };
```