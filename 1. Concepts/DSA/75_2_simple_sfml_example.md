### 75.2 Simple SFML Example

```cpp
#include <SFML/Graphics.hpp>

int main() {
    sf::RenderWindow window(sf::VideoMode(800, 600), "Game");
    sf::CircleShape circle(50);
    while (window.isOpen()) {
        sf::Event event;
        while (window.pollEvent(event))
            if (event.type == sf::Event::Closed) window.close();
        window.clear();
        window.draw(circle);
        window.display();
    }
}
```

---