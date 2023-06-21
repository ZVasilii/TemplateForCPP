cmake_minimum_required(VERSION 3.22)
project(DummyProject)

if("${CMAKE_BINARY_DIR}" STREQUAL "${CMAKE_SOURCE_DIR}")
  message(
    FATAL_ERROR
      "In-source builds are disabled.
  Please create a subfolder and use `cmake ..` inside it.
  NOTE: cmake will now create CMakeCache.txt and CMakeFiles/*.
  You must delete them, or cmake will refuse to work.")
endif()

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

# indicate the docs build
option(BUILD_DOC "Build docs" OFF)
# indicate the tests build
option(BUILD_TESTS "Build tests" OFF)

message("Project: ${PROJECT_NAME}")
message("Build Type: ${CMAKE_BUILD_TYPE}")
if(BUILD_DOC)
  message("Documentation build enabled")
endif()
if(BUILD_TESTS)
  message("Unit-tests build enabled")
endif()

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_FLAGS_RELEASE "-O2 -Wall -Wextra -Wpedantic")
set(CMAKE_CXX_FLAGS_DEBUG "-g -O0 -Wall -Wextra -Wpedantic")

#Tests:

include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)
FetchContent_MakeAvailable(googletest)
add_library(GTest::GTest INTERFACE IMPORTED)
target_link_libraries(GTest::GTest INTERFACE gtest_main)

if(BUILD_TESTS)
  enable_testing()
endif()

add_subdirectory(tests)
target_link_libraries(DummyTest GTest::gtest_main)
include(GoogleTest)
add_test(DummyTest tests/DummyTest)


#Compile:

add_executable( ${PROJECT_NAME}
    main.cc
)

add_subdirectory(src)
target_include_directories(${PROJECT_NAME} PRIVATE include)
target_include_directories(${PROJECT_NAME} PRIVATE src)
target_link_libraries(${PROJECT_NAME} DummyTarget)

#Docs:
add_subdirectory(docs)
