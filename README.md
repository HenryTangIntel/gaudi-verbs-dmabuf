# gaudi-verbs-dmabuf

A client-server implementation for DMA buffer operations using RDMA verbs on Habana Gaudi hardware.

## Overview

This project demonstrates how to use RDMA (Remote Direct Memory Access) verbs with DMA buffers on Habana Gaudi hardware. It consists of a client and server implementation that establish a connection and perform memory operations directly between devices.

## Prerequisites

- Habana Gaudi hardware
- RDMA-capable network infrastructure
- Ubuntu Linux (tested on Ubuntu 22.04 LTS)
- CMake (3.22+)
- C++ compiler with C++11 support
- Habana SynapseAI software stack
- RDMA verbs libraries (`libibverbs`, `librdmacm`)

## Building the Project

```bash
# Create build directory (if it doesn't exist)
mkdir -p build

# Navigate to build directory
cd build

# Generate build files with CMake
cmake ..

# Build the project
make
```

## Usage

### Running the Server

```bash
./build/server [options]
```

### Running the Client

```bash
./build/client [server-address] [options]
```

## Project Structure

- `include/` - Header files
  - `client.hpp` - Client class declaration
  - `server.hpp` - Server class declaration
  - `hpuverbs.hpp` - RDMA verbs abstraction for Habana devices

- `src/` - Source files
  - `client.cpp` - Client implementation
  - `server.cpp` - Server implementation
  - `hpuverbs.cpp` - RDMA verbs implementation

## License

[Insert license information here]

## Contributing

[Insert contribution guidelines here]

## Contact

[Insert contact information here]