cmake_minimum_required(VERSION 3.25)
project(arcdps_addon_2)

set(CMAKE_CXX_STANDARD 17)

# Compiler-specific options for GCC
if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    # -static-libgcc -static-libstdc++ fixes the "missing" libgcc_s_seh-1.dll and libstdc++-6.dll
    # -static alone should fix the "missing" libwinpthread-1.dll
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -static-libgcc -static-libstdc++ -static")
endif()

file(GLOB IMGUI_SOURCES imgui/*.cpp imgui/*.h)
add_library(imgui STATIC ${IMGUI_SOURCES})
target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/imgui)

add_library(arcdps_addon_2 SHARED arcdps_combatdemo.cpp)
target_link_libraries(arcdps_addon_2 imgui)
