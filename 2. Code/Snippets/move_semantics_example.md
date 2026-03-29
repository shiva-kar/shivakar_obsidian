### Move semantics example

```cpp
#include <string>
#include <utility>

struct S {
    std::string data;
    S(std::string d): data(std::move(d)) {}
    S(S&&) = default;
    S& operator=(S&&) = default;
};
```