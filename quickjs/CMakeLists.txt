cmake_minimum_required(VERSION 3.27)

if(CMAKE_GENERATOR MATCHES "Visual Studio")
    message(FATAL_ERROR "MSVC is not supported.")
endif()

if(WIN32)
    set(CMAKE_GNUtoMS ON)
endif()

project(quickjs LANGUAGES C)

file(STRINGS "VERSION" QJS_VERSION)

add_library(quickjs SHARED
    cutils.c
    libbf.c
    libregexp.c
    libunicode.c
    quickjs.c)

target_compile_options(quickjs PRIVATE -O3)
target_compile_definitions(quickjs PRIVATE
    NDEBUG
    _GNU_SOURCE
    CONFIG_BIGNUM
    CONFIG_VERSION="\\\"${QJS_VERSION}\\\"")

target_link_options(quickjs PRIVATE -static)
target_link_libraries(quickjs PRIVATE pthread)
