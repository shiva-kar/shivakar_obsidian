### 72.1 Text-Based (JSON, XML)

- Libraries: nlohmann/json, rapidjson, pugixml
    

```cpp
#include <nlohmann/json.hpp>
#include <iostream>
using json = nlohmann::json;

int main() {
    json j = { {"name", "Alice"}, {"age", 25} };
    std::cout << j.dump(4);
}
```