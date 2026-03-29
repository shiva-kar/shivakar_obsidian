## 24. Standard Template Library (STL)

- Containers: `std::vector`, `std::string`, `std::deque`, `std::list`, `std::set`, `std::map`, `std::unordered_map`
    
- Iterators and iterator categories
    
- Algorithms: `<algorithm>` e.g., `std::sort`, `std::find`, `std::transform`
    
- `std::tuple`, `std::pair`
    
- Example:
    

```cpp
#include <vector>
#include <algorithm>

std::vector<int> v{3,1,4,1,5};
std::sort(v.begin(), v.end());
```