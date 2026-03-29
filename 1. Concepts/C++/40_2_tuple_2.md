### 40.2 `<tuple>`

- `std::tuple<Ts...>` for grouping heterogeneous values.
    
- Access with `std::get<N>`.
    
- Structured binding (C++17):
    

```cpp
#include <tuple>
#include <iostream>

auto person = std::make_tuple("Alice", 20, 5.7);
auto [name, age, height] = person;
std::cout << name << " " << age << " " << height;
```