cmake_minimum_required(VERSION 3.10)

project(nfd)

if(WIN32)
    set(NFD_PLATFORM_SOURCE src/nfd_win.cpp)
endif()

add_library(${PROJECT_NAME} STATIC
    src/nfd_common.c
    ${NFD_PLATFORM_SOURCE}
)
add_library(nfd::nfd ALIAS ${PROJECT_NAME})
target_include_directories(${PROJECT_NAME}
    PUBLIC src/include
)

add_subdirectory(test)
