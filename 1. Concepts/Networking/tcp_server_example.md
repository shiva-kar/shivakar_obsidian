# TCP Server Example

## Core Idea
Concise explanation of the concept and when to use it.

## Why it exists
Problem this concept solves in real systems.

## Mental Model
One-line mental picture for quick recall.

## Code Pattern
~~~c
// key pattern or API usage
~~~

## Common Mistakes
- Misusing API/state assumptions

## Interview Angle
- Typical questions and tradeoffs

## Related
- [[network_programming]]
- [[sockets]]

## Legacy Notes (archived)
### 68.2 TCP Server Example (Boost.Asio)

```cpp
#include <boost/asio.hpp>
using boost::asio::ip::tcp;

int main() {
    boost::asio::io_context io;
    tcp::acceptor acceptor(io, tcp::endpoint(tcp::v4(), 8080));
    tcp::socket socket(io);
    acceptor.accept(socket);
    boost::asio::write(socket, boost::asio::buffer("Hello, Client\n"));
}
```


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

