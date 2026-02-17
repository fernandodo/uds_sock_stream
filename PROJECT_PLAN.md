# UDS SOCK_STREAM Study Project Plan

This project aims to implement a Unix Domain Socket (UDS) Server and Client in C++ to understand system-level IPC (Inter-Process Communication).

## Phase 1: Architecture & Setup
- **Project Structure**:
  - `src/common`: Shared headers (socket paths, constants, utility classes).
  - `src/server`: Server-specific logic.
  - `src/client`: Client-specific logic.
- **Build System**: Use CMake to manage compilation and flags (`-Wall -Wextra -pthread`).
- **RAII Wrappers**: Develop a C++ class for socket file descriptor management to ensure resources are freed automatically.

## Phase 2: Server Implementation
1. **Initialization**: Create socket using `AF_UNIX` and `SOCK_STREAM`.
2. **Address Binding**: Configure `sockaddr_un`. Ensure `unlink()` is called before `bind()`.
3. **Lifecycle**:
   - `listen()`: Establish a backlog for incoming connections.
   - `accept()`: Wait for and accept client connections.
4. **Communication**: Implement a message-based protocol using `read()` and `write()`.

## Phase 3: Client Implementation
1. **Connection**: Create socket and `connect()` to the predefined path.
2. **Interaction**: Implement logic to send requests and process server responses.
3. **Robustness**: Handle connection failures and missing socket files gracefully.

## Phase 4: Advanced Concepts
- **Error Handling**: Wrap `errno` with `std::system_error`.
- **Signal Management**: Handle/ignore `SIGPIPE`.
- **Buffer Safety**: Use modern C++ containers (`std::vector`, `std::string_view`) for data handling.
- **Concurrency**: (Optional) Multi-threaded handling for concurrent clients.

## Phase 5: Verification
- **Integration**: Run server/client pair.
- **Stress Test**: Verify behavior under load and with large payloads.
