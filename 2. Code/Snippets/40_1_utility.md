### 40.1 `<utility>`

- `std::pair`, `std::move`, `std::forward`, `std::swap`
    
- `std::exchange`: assigns a new value and returns the old one.
    

```cpp
#include <utility>
int x = 10;
int y = std::exchange(x, 20); // y=10, x=20
```