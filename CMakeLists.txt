cmake_minimum_required(VERSION 3.10)

project(nfd)

if(WIN32)
    set(NFD_PLATFORM_SOURCE src/nfd_win.cpp)
endif()

if(APPLE)
    # https://stackoverflow.com/questions/3770498/cmake-compile-with-frameworks-on-mac-osx-and-treat-cpp-files-like-m-mm
    set(NFD_PLATFORM_SOURCE src/nfd_cocoa.m)
    set_source_files_properties(${NFD_PLATFORM_SOURCE} PROPERTIES
                            COMPILE_FLAGS "-x objective-c")
endif()

add_library(${PROJECT_NAME} STATIC
    src/nfd_common.c
    ${NFD_PLATFORM_SOURCE}
)

add_library(nfd::nfd ALIAS ${PROJECT_NAME})
target_include_directories(${PROJECT_NAME}
    PUBLIC src/include
)

if(APPLE)
    # https://stackoverflow.com/questions/20962869/cmakelists-txt-for-an-objective-c-project
    target_link_libraries(nfd
        "-framework Cocoa"
        "-framework AppKit"
        "-framework CoreData"
        "-framework Foundation"
    )
endif()

option(NFD_BUILD_TESTS "Build the tests" YES)
if(NFD_BUILD_TESTS)
    add_subdirectory(test)
endif()