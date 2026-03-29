### Lambda + STL example

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{3,1,4,1,5};
    std::sort(v.begin(), v.end(), [](int a, int b){ return a < b; });
    for (int x : v) std::cout << x << ' ';
}
```