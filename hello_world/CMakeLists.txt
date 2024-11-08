cmake_minimum_required(VERSION 3.16)

project(hello_world)

find_package(absl REQUIRED)

add_executable(hello_world hello_world.cc)

target_include_directories(hello_world PUBLIC "/usr/local/lib/")

target_link_libraries(hello_world absl::strings)
