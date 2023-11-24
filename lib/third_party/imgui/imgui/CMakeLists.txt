cmake_minimum_required(VERSION 3.16)
# https://github.com/ocornut/imgui
project(imgui_imgui)

set(CMAKE_CXX_STANDARD 17)

add_library(imgui_imgui OBJECT
        source/imgui.cpp
        source/imgui_demo.cpp
        source/imgui_draw.cpp
        source/imgui_tables.cpp
        source/imgui_widgets.cpp

        source/misc/freetype/imgui_freetype.cpp
)

target_include_directories(imgui_imgui PUBLIC
    include
    include/misc/freetype
)

add_library(imgui_includes INTERFACE)
target_include_directories(imgui_includes INTERFACE include)

target_compile_options(imgui_imgui PRIVATE -Wno-unknown-warning-option)
set_property(TARGET imgui_imgui PROPERTY POSITION_INDEPENDENT_CODE ON)

find_package(Freetype REQUIRED)

target_include_directories(imgui_imgui PUBLIC ${FREETYPE_INCLUDE_DIRS})
target_link_directories(imgui_imgui PUBLIC ${FREETYPE_LIBRARY_DIRS})
target_link_libraries(imgui_imgui PUBLIC ${FREETYPE_LIBRARIES})