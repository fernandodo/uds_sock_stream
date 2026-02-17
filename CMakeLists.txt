cmake_minimum_required(VERSION 3.10)
project(uds_sock_stream VERSION 0.0.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(sock_stream_server src/server/main.cpp)
add_executable(sock_stream_client src/client/main.cpp)

# global include directories
include_directories(src/common)

# target include directories
target_include_directories(sock_stream_server PRIVATE src/server)
target_include_directories(sock_stream_client PRIVATE src/client)

# compile warnings
target_compile_options(sock_stream_server PRIVATE -Wall -Wextra -Wpedantic)
target_compile_options(sock_stream_client PRIVATE -Wall -Wextra -Wpedantic)