## 9. Arrays & std::array / std::vector

- C-style arrays still present
    
- Prefer `std::array<T, N>` for fixed-size arrays
    
- Prefer `std::vector<T>` for dynamic arrays (safer, RAII)
    
- Multidimensional arrays vs `std::vector<std::vector<T>>`
    

```cpp
#include <vector>
std::vector<int> v = {1,2,3};
v.push_back(4);
```