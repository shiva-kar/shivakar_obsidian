## 25. Function Pointers, std::function & Callables

- Function pointers exist
    
- `std::function` and `std::bind`, lambdas for higher-level callables
    

```cpp
#include <functional>
std::function<int(int,int)> op = [](int a,int b){ return a+b; };
```