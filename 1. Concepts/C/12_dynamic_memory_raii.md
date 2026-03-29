## 12. Dynamic Memory & RAII

- Prefer RAII: resources owned by objects and freed in destructors
    
- Raw `new`/`delete` are legal but discouraged
    
- Use smart pointers (`std::unique_ptr`, `std::shared_ptr`, `std::weak_ptr`)
    
- `std::make_unique`, `std::make_shared`
    

```cpp
#include <memory>

auto p = std::make_unique<int>(42); // unique_ptr<int>
```