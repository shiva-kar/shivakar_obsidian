### 65.2 Example (Catch2)

```cpp
#define CATCH_CONFIG_MAIN
#include "catch.hpp"
int add(int a, int b){ return a+b; }
TEST_CASE("Addition", "[math]") {
    REQUIRE(add(2,3) == 5);
}
```

---