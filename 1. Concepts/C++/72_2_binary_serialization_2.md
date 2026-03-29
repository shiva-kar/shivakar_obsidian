### 72.2 Binary Serialization

- Use `<fstream>` or libraries like cereal, protobuf.
    

```cpp
#include <cereal/archives/binary.hpp>
#include <fstream>

struct Data { int x; template<class Ar> void serialize(Ar& ar){ ar(x); } };
```

---