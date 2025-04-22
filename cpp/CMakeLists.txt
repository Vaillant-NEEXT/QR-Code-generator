cmake_minimum_required(VERSION 3.22)

project(qrcodegen LANGUAGES CXX VERSION 1.8)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
if(CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    add_compile_options(/W4 /EHsc)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    add_compile_options(-Wall -Wextra -Wno-unused-parameter -Wno-missing-field-initializers -Wcast-qual -Wconversion -Wshadow)
endif()


add_library(${PROJECT_NAME} STATIC
    qrcodegen.hpp
    qrcodegen.cpp
)

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_LIST_DIR})
