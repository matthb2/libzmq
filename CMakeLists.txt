project(libzmq)
cmake_minimum_required(VERSION 2.6)
enable_testing()

find_package(Threads REQUIRED)

add_subdirectory(src)
add_subdirectory(tests)
