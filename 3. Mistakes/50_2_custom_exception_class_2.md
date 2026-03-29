### 50.2 Custom Exception Class

```cpp
#include <stdexcept>
class FileError : public std::runtime_error {
public:
    explicit FileError(const std::string &msg) : std::runtime_error(msg) {}
};
```