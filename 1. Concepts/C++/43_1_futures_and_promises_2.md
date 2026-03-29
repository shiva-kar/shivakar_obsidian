### 43.1 Futures and Promises

```cpp
#include <future>
#include <iostream>

int compute() { return 42; }

int main() {
    std::future<int> result = std::async(compute);
    std::cout << result.get(); // waits for completion
}
```