## 49. Complete Sample Program (Combines Multiple Concepts)

```cpp
#include <iostream>
#include <vector>
#include <memory>
#include <algorithm>

class Shape {
public:
    virtual double area() const = 0;
    virtual ~Shape() = default;
};

class Circle : public Shape {
    double r;
public:
    explicit Circle(double radius): r(radius) {}
    double area() const override { return 3.14159 * r * r; }
};

class Rectangle : public Shape {
    double w, h;
public:
    Rectangle(double width, double height): w(width), h(height) {}
    double area() const override { return w * h; }
};

int main() {
    std::vector<std::unique_ptr<Shape>> shapes;
    shapes.push_back(std::make_unique<Circle>(5.0));
    shapes.push_back(std::make_unique<Rectangle>(3.0, 4.0));

    double total = 0;
    for (auto& s : shapes) total += s->area();
    std::cout << "Total area: " << total << '\n';
}
```

**Demonstrates:** classes, inheritance, virtual functions, smart pointers, STL container, loop, polymorphism, RAII.