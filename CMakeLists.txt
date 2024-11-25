cmake_minimum_required(VERSION 3.12.0)
project(PDCurses VERSION 0.1.0 LANGUAGES C)

option(WIDE "Export wchar functions" ON)
option(UTF8 "Force utf-8 format" ON)

if (WIDE)
    add_compile_options(-DPDC_WIDE)
endif()

if (UTF8)
    add_compile_options(-DPDC_FORCE_UTF8)
endif()

add_compile_options(-O2 -w)

file(GLOB SOURCES CONFIGURE_DEPENDS ./pdcurses/*.c)

if(WIN32)
    file(GLOB SOURCES_PLATFORM CONFIGURE_DEPENDS ./wincon/*.c)
    set(INCLUDES ./wincon)
endif()

add_library(PDCurses STATIC ${SOURCES} ${SOURCES_PLATFORM})

target_include_directories(PDCurses PRIVATE ${INCLUDES})
target_include_directories(PDCurses PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(PDCurses PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/common)
