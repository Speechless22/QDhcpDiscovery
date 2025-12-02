cmake_minimum_required(VERSION 3.16)
project(QDhcpDiscovery VERSION 1.0 LANGUAGES CXX)

find_package(Qt6 REQUIRED COMPONENTS Core Network)

qt_standard_project_setup()

add_subdirectory(lib)
add_subdirectory(example)
add_subdirectory(test)
