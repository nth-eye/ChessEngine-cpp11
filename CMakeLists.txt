cmake_minimum_required(VERSION 3.0.0)
project(chess VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)
set(CMAKE_CXX_FLAGS "-Wall -Wextra -Wpedantic -Ofast")
set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})

include_directories(inc)
file(GLOB SRC_FILES src/*.cpp)
add_executable(chess main.cpp ${SRC_FILES})

include(FetchContent)
FetchContent_Declare(googletest URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip)
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

enable_testing()
file(GLOB TEST_FILES test/*.cpp) 
add_executable(chess_test ${TEST_FILES} ${SRC_FILES})
target_link_libraries(chess_test gtest_main)
include(GoogleTest)
gtest_discover_tests(chess_test)