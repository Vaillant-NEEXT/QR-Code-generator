cmake_minimum_required(VERSION 3.22)

project(qrcodegen LANGUAGES CXX VERSION 1.8)

option(SHARED_LIB "Build as shared libraries" NO)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
if(CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    add_compile_options(/W4 /EHsc)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    add_compile_options(-Wall -Wextra -Wno-unused-parameter -Wno-missing-field-initializers -Wcast-qual -Wconversion -Wshadow)
endif()


set(SOURCES qrcodegen.cpp)
set(HEADERS qrcodegen.hpp)

if(SHARED_LIB)
    if(MSVC)
        set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
    endif()
    add_library(${PROJECT_NAME} SHARED ${SOURCES} ${HEADERS})
    set_target_properties(${PROJECT_NAME} PROPERTIES VERSION ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH} SOVERSION ${PROJECT_VERSION_MAJOR})
else()
    add_library(${PROJECT_NAME} STATIC ${SOURCES} ${HEADERS})
endif()


## Install the library
include(GNUInstallDirs)
install(FILES ${HEADERS} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(TARGETS ${PROJECT_NAME} DESTINATION ${CMAKE_INSTALL_LIBDIR})

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_LIST_DIR})
