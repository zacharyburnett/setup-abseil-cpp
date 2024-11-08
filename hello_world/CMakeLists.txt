cmake_minimum_required(VERSION 3.16)

project(hello_world)

find_package(PkgConfig REQUIRED)
pkg_check_modules(ABSEIL REQUIRED abseil)

add_executable(hello_world hello_world.cc)

target_include_directories(hello_world PUBLIC ${ABSEIL_INCLUDE_DIRS})
target_link_libraries(hello_world ${ABSEIL_LIBRARIES})

# Declare dependency on the absl::strings library
target_link_libraries(hello_world absl::strings)
