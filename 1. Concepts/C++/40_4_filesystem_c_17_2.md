### 40.4 `<filesystem>` (C++17)

- Filesystem API for paths, directories, file iteration.
    
- Example:
    

```cpp
#include <filesystem>
#include <iostream>
namespace fs = std::filesystem;

int main() {
    for (auto &p : fs::directory_iterator(".")) 
        std::cout << p.path() << '\n';
}
```

---