cmake_minimum_required(VERSION 3.12.0)
project(PDCurses VERSION 0.1.0 LANGUAGES C)

add_compile_options(-O2 -w)

file(GLOB SOURCES CONFIGURE_DEPENDS ./pdcurses/*.c)

if(WIN32 OR MSVC)
    file(GLOB SOURCES_PLATFORM CONFIGURE_DEPENDS ./wincon/*.c)
    set(INCLUDES ./wincon)
endif()

add_library(PDCurses STATIC ${SOURCES} ${SOURCES_PLATFORM})

target_include_directories(PDCurses PRIVATE ${INCLUDES})
target_include_directories(PDCurses PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(PDCurses PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/common)
