## 31. Operator Overloading

- Overload operators as member or non-member functions
    
- Common overloads: `operator+`, `operator=`, `operator<<` (stream insertion)
    
- Keep semantics intuitive
    

```cpp
#include <iostream>

struct Vec {
    int x,y;
    Vec(int a,int b):x(a),y(b){}
    Vec operator+(const Vec& o) const { return Vec(x+o.x,y+o.y); }
};

std::ostream& operator<<(std::ostream& os, const Vec& v) {
    return os << '(' << v.x << ',' << v.y << ')';
}
```