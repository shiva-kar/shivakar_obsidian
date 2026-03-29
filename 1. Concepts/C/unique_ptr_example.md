### unique_ptr example

```cpp
#include <memory>
#include <iostream>

struct Node { int v; std::unique_ptr<Node> next; };

int main() {
    auto head = std::make_unique<Node>();
    head->v = 1;
    head->next = std::make_unique<Node>();
    head->next->v = 2;
}
```