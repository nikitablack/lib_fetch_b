cmake_minimum_required(VERSION 3.18 FATAL_ERROR)

project(lib_fetch_b LANGUAGES CXX)

include(FetchContent)

set(LIB_FETCH_A_VERSION 6afc92b679adec75dc6c6adb7bfbd005d987a127)
message(STATUS "Downloading lib_fetch_a ${LIB_FETCH_A_VERSION}")

FetchContent_Declare(lib_fetch_a
    GIT_REPOSITORY git@github.com:nikitablack/lib_fetch_a.git
    GIT_TAG ${LIB_FETCH_A_VERSION}
    SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR}/third_party/lib_fetch_a
)

FetchContent_MakeAvailable(lib_fetch_a)

add_library(lib_fetch_b SHARED
    src/bar.cpp
)

set_target_properties(lib_fetch_b PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
)

target_include_directories(lib_fetch_b PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_link_libraries(lib_fetch_b PUBLIC lib_fetch_a)
