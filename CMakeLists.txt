cmake_minimum_required(VERSION 3.14)
project(cz5test C CXX)

message(STATUS "Using C11")
set(CMAKE_C_STANDARD 11)

if (NOT "${CMAKE_CXX_FLAGS}" MATCHES "-std=c\\+\\+17")
    message(STATUS "Using C++14")
    set(CMAKE_CXX_STANDARD 14)
else()
    message(STATUS "Using C++17")
endif()
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(DEFINED ENV{CONDA_PREFIX})
    include_directories(BEFORE $ENV{CONDA_PREFIX}/include)
    list(APPEND CMAKE_PREFIX_PATH $ENV{CONDA_PREFIX})
endif()

find_package(Boost REQUIRED COMPONENTS filesystem)

add_executable(test_cpp main.cpp)
target_link_libraries(test_cpp LINK_PUBLIC Boost::filesystem)

add_executable(test_c main.c z5wrapper.cc)