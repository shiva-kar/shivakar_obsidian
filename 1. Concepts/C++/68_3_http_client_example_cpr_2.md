### 68.3 HTTP Client Example (cpr)

```cpp
#include <cpr/cpr.h>
#include <iostream>

int main() {
    auto r = cpr::Get(cpr::Url{"https://example.com"});
    std::cout << r.status_code << "\n" << r.text;
}
```

---