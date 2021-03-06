cmake_minimum_required(VERSION 3.10)
project(lua VERSION 5.4.1 DESCRIPTION "CMake compatible Lua library")

option(BUILD_SHARED_LIBS "Build shared libraries" ON)

if (BUILD_SHARED_LIBS)
    set(LIB_TYPE SHARED)
    if (MSVC)
        add_definitions(-DLUA_BUILD_AS_DLL)
    endif ()
else ()
    set(LIB_TYPE STATIC)
    if (MSVC)
        add_definitions(-ULUA_BUILD_AS_DLL)
    endif ()
endif ()

file(GLOB_RECURSE SOURCES src/*.c)
add_library(lua ${LIB_TYPE} ${SOURCES})

target_include_directories(lua PUBLIC include)

install(TARGETS lua DESTINATION lib)
file(GLOB_RECURSE INCLUDES include/*.h include/*.hpp)
install(FILES ${INCLUDES} DESTINATION include)
