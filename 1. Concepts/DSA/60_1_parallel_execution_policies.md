### 60.1 Parallel Execution Policies

`std::execution::seq`, `std::execution::par`, `std::execution::par_unseq`

```cpp
#include <execution>
#include <algorithm>
std::sort(std::execution::par, v.begin(), v.end());
```

---