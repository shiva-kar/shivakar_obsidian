### 40.3 `<chrono>` (Time)

- Types: `std::chrono::duration`, `std::chrono::time_point`
    
- Clock types: `system_clock`, `steady_clock`, `high_resolution_clock`
    
- Usage:
    

```cpp
#include <chrono>
#include <thread>
#include <iostream>

auto start = std::chrono::steady_clock::now();
std::this_thread::sleep_for(std::chrono::seconds(1));
auto end = std::chrono::steady_clock::now();
std::cout << std::chrono::duration_cast<std::chrono::milliseconds>(end - start).count() << "ms";
```