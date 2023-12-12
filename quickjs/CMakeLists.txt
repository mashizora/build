cmake_minimum_required(VERSION 3.27)

if(CMAKE_GENERATOR MATCHES "Visual Studio")
    message(FATAL_ERROR "MSVC is not supported, use MSYS2 for windows build.")
endif()

if(WIN32)
    set(CMAKE_GNUtoMS ON)
endif()

project(quickjs LANGUAGES C)

set(CFLAGS -Wall -Wextra)

list(APPEND CFLAGS -O3 -flto=auto)

file(STRINGS "VERSION" QJS_VERSION)

add_library(quickjs SHARED
            cutils.c
            libbf.c
            libregexp.c
            libunicode.c
            quickjs.c)


target_compile_options(quickjs PRIVATE ${CFLAGS})
target_compile_definitions(quickjs PRIVATE
                            NDEBUG
                            _GNU_SOURCE
                            CONFIG_BIGNUM
                            CONFIG_VERSION="\\\"${QJS_VERSION}\\\"")

