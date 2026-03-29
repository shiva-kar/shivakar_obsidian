### 77.2 Python Integration

- **pybind11** and **Boost.Python**
    

```cpp
#include <pybind11/pybind11.h>
int add(int a, int b){ return a+b; }
PYBIND11_MODULE(example, m){ m.def("add", &add); }
```