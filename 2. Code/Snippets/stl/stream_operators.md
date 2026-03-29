### 58.1 Overloading Stream Operators

```cpp
class Point {
public:
    int x, y;
};
std::ostream& operator<<(std::ostream& os, const Point& p){
    return os << "(" << p.x << "," << p.y << ")";
}
```