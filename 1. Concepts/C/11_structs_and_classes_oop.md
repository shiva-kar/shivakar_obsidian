## 11. Structs and Classes (OOP)

- `struct` vs `class` (default public vs private)
    
- Access specifiers: `public`, `protected`, `private`
    
- Member functions, data members
    
- Constructors, destructors
    
- `this` pointer
    
- `friend` functions/classes
    
- Example:
    

```cpp
#include <string>
#include <iostream>

class Person {
public:
    Person(std::string n, int a): name(std::move(n)), age(a) {}
    void greet() const { std::cout << "Hi, I'm " << name << '\n'; }
private:
    std::string name;
    int age;
};
```