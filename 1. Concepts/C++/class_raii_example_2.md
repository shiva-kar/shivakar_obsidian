### Class + RAII example

```cpp
#include <iostream>
#include <fstream>
#include <string>

class Logger {
    std::ofstream out;
public:
    Logger(const std::string &file): out(file) {}
    void log(const std::string &s) { out << s << '\n'; }
    // destructor closes ofstream automatically
};
```