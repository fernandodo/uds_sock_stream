# Technical Specification: UDS SOCK_STREAM Study

This document defines the behavior and requirements for the Unix Domain Socket (UDS) stream server and client.

## 1. Connection Details
- **Socket Family**: `AF_UNIX` (Unix Domain Sockets).
- **Socket Type**: `SOCK_STREAM` (Connection-oriented, reliable byte stream).
- **Socket Path**: `/tmp/uds_stream.sock` (Default).
- **Cleanup**: The server must `unlink()` the socket path before binding to ensure a fresh start.

## 2. Communication Protocol
*To be finalized. Proposed options:*
- **Option A (Delimiter-based)**: Messages end with a `
` character. Simple for testing with `nc -U`.
- **Option B (Length-Prefix)**: Each message is preceded by a 4-byte header (integer) indicating the payload size. More robust for complex data.
- **Decision**: (Recommended: Start with Delimiter-based for simplicity, then evolve to Length-Prefix).

## 3. Server Architecture
- **Concurrency**: 
  - Iteration 1: **Sequential** (Handles one client at a time).
  - Iteration 2: **Multi-threaded** (Spawns a `std::thread` per accepted connection).
- **Backlog**: The listen queue shall be set to 5.

## 4. Business Logic (The "Echo" Service)
- The server shall read data from the client.
- The server shall send the received data back to the client exactly as it was received.
- **Termination Command**: If the client sends the string `QUIT
`, the server should close that specific connection.

## 5. Error Handling
- **System Calls**: Every socket API call (`socket`, `bind`, `listen`, `accept`, `connect`, `read`, `write`) must be checked for error results (-1).
- **Exceptions**: Use `std::system_error` to wrap `errno` for idiomatic C++ error propagation.
- **SIGPIPE**: The application must ignore or handle `SIGPIPE` to prevent crashes when writing to a closed socket.

## 6. Lifecycle Management
- **Server Shutdown**: On graceful exit, the server should close the listening socket and remove the socket file from the filesystem.
- **Client Exit**: The client should close the connection gracefully.
