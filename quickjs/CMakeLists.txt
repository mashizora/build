cmake_minimum_required(VERSION 3.27)

if(WIN32)
    set(CMAKE_GNUtoMS ON)
    string(APPEND CMAKE_C_FLAGS " -static")
endif()

project(quickjs LANGUAGES C)

file(STRINGS "VERSION" QJS_VERSION)

add_library(quickjs SHARED
            cutils.c
            libbf.c
            libregexp.c
            libunicode.c
            quickjs.c)



target_compile_definitions(quickjs PRIVATE
                            _GNU_SOURCE
                            CONFIG_BIGNUM
                            CONFIG_VERSION="\\\"${QJS_VERSION}\\\""
                            )
