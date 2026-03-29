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