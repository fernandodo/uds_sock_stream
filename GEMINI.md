# UDS SOCK_STREAM Study Project

This project is a study of Unix Domain Sockets (UDS) using C++. It implements a connection-oriented (`SOCK_STREAM`) server and client to understand Inter-Process Communication (IPC) on Linux.

## Project Structure

- `src/common/`: Shared headers (RAII socket wrappers, protocol definitions).
- `src/server/`: Server implementation logic and main entry point.
- `src/client/`: Client implementation logic and main entry point.
- `docs/`: Documentation and Q&A regarding project decisions.
- `CMakeLists.txt`: Build configuration for the project.
- `PROJECT_PLAN.md`: Development roadmap.
- `SPEC.md`: Technical specification and protocol details.

## Current Progress

- [x] Project structure and Git initialization.
- [x] CMake configuration and compiler flags.
- [x] Technical specification (SPEC.md) and development plan (PROJECT_PLAN.md).
- [ ] Implementation of RAII Socket Wrapper.
- [ ] Server implementation.
- [ ] Client implementation.

## How to Build

Once the source code is implemented, use the following commands:

```bash
mkdir -p build && cd build
cmake ..
make
```

## How to Run

After building, you will have two binaries in the `build/` directory:
- `./sock_stream_server`
- `./sock_stream_client`

