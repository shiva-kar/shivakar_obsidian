### 73.1 Simple Logging

```cpp
#include <iostream>
#define LOG(x) std::cout << __FILE__ << ":" << __LINE__ << " " << x << "\n"
```