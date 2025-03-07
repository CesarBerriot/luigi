cmake_minimum_required(VERSION 3.30)
project(luigi C)

if(NOT WIN32 AND NOT UNIX)
    message(FATAL_ERROR "Unsupported platform.")
endif()

add_library(luigi source/luigi.c)
target_include_directories(luigi PUBLIC include)

if(WIN32)
    target_compile_definitions(luigi PUBLIC UI_WINDOWS)
    target_link_libraries(luigi PRIVATE user32.lib gdi32.lib shell32.lib)
else()
    # untested
    target_compile_definitions(luigi PUBLIC UI_LINUX)
    target_link_libraries(luigi PRIVATE X11 m)
endif()

