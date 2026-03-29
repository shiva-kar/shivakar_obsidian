### Template function

```cpp
#include <iostream>

template<typename T>
T add(T a, T b) { return a + b; }

int main() {
    std::cout << add<int>(2,3) << '\n';
}
```