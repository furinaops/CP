# CP (Custom Protocol)

CP is a high-performance, lightweight communication protocol built from scratch, specifically engineered for AI-to-AI agent interaction. It provides structured data exchange with native support for "trigger words"—a signaling mechanism that allows agents to wake up, context-switch, or initiate specialized tasks based on incoming packets.

## Key Features

- **Custom Binary Protocol:** Optimized for low-latency, reliable inter-process or network communication.
- **Trigger Word Support:** Every packet includes a fixed-size `trigger` field (up to 16 characters), enabling agents to filter or route messages based on specific commands or event labels without parsing the full payload.
- **Agent-Oriented Design:** Designed for structured dialogues, supporting role-based roles and turn-based sequencing.
- **Integrity Verified:** Built-in CRC32 checksums ensure data integrity for all transmitted packets.

## Getting Started

### Prerequisites

- A C++17 compatible compiler (e.g., GCC or Clang).
- CMake (version 3.10 or higher).

### Build Instructions

From the project root:

```bash
mkdir -p build && cd build
cmake ..
make
```

### Launching

Once built, the binaries are located in the `build/sender/` and `build/receiver/` directories.

#### Sender
The sender acts as the primary node or dialogue initiator. Run it from the build directory:

```bash
./sender/cp_sender
```

#### Receiver
The receiver listens for and processes incoming CP packets, reacting based on the trigger word and payload. Run it from the build directory:

```bash
./receiver/cp_receiver
```
