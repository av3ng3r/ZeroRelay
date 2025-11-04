# zerorelay

**zerorelay** is an open source, high-performance WebSocket relay server built with C++ using Boost.Asio and Boost.Beast. It enables real-time, low-latency messaging for applications such as chat systems, live notifications, multiplayer games, and distributed event streaming.

---

## Features

- Efficient asynchronous WebSocket handling with Boost.Beast  
- Secure client authentication via token-based mechanisms  
- Publish/Subscribe message routing  
- Backpressure and slow consumer detection to maintain stability  
- Rate limiting per connection and per tenant  
- Prometheus metrics with Grafana dashboard integration  
- Containerized deployment with Docker, Docker Compose, and Helm charts for Kubernetes  

---

## Architecture

_Architecture diagram coming soon._  

Key components will include:
- WebSocket gateway managing client connections with concurrency control via Boost.Asio strands  
- A core relay router for topic management and message fanout  
- Metrics and health endpoints exposing observability data  

---

## Quickstart

### Prerequisites
- C++17 compatible compiler (GCC 10 or newer recommended)
- CMake 3.20 or higher
- Python 3 and pip for Conan package manager
- Docker (optional, for containerized deployment) 

### Clone and Build

```
git clone https://github.com/yourusername/zerorelay.git
cd zerorelay

# Install dependencies with Conan
pip install --user conan
conan install . --build=missing --output-folder=build/conan

# Configure CMake with Conan toolchain and set build type
cmake -S . -B build -DCMAKE_TOOLCHAIN_FILE=build/conan/conan_toolchain.cmake -DCMAKE_BUILD_TYPE=Release

# Build the project
cmake --build build

```

### Run the executable
```
./build/ZeroRelay
```
Or run with Docker Compose:
```
docker-compose up
```

### Testing
Connect a WebSocket client like wscat to ws://localhost:8080 and send messages to test the relay functionality.

---

## Roadmap

### Milestone 1 (Core MVP - 2 weeks)
- Async WebSocket server with Boost.Beast  
- Authentication scaffold with JWT/HMAC tokens  
- Basic publish/subscribe routing  
- Per-connection backpressure and bounded queues  
- Prometheus metrics endpoint and Grafana dashboard  

### Milestone 2 (Extended Features - 4 weeks)
- At-least-once delivery mode with acknowledgments  
- Rate limiting and quotas per tenant  
- REST admin APIs for token management  
- Containerization with Helm charts  

### Milestone 3 (Polish and Community - 6 weeks+)
- Additional client SDKs (Go, Python)  
- Extensive documentation including architecture and protocol specs  
- Load testing and benchmarks published  
- Community contribution guidelines and issue triage  

---

## Contribution

_coming soon._

<!-- We welcome contributions! Please follow the steps below:

1. Fork the repository  
2. Create a feature branch (`git checkout -b feature-name`)  
3. Write tests and update documentation  
4. Submit a pull request  

See [CONTRIBUTING.md](CONTRIBUTING.md) for full guidelines.-->

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Contact

For questions or discussion, please open an issue or join the project Slack channel (coming soon).
