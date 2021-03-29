# GoogleTest
A builtin CMake module defines functions to help use the Google Test

## Two ways to find gtest
### FindGTest.cmake
Builtin CMake find module, used in `find_package()` module mode

This script defines:
* `IMPORTED` targets
    - `GTest::GTest`, `GTest::Main` (before CMake 3.20)
    - `GTest::gtest`, `GTest::gtest_main` (since CMake 3.20)
    - `gtest_main` target can be linked to avoid writing my own `main` function

### GTestConfig.cmake
Shipped with GTest latest version (1.10), Ubuntu 18.04 has a gtest version 1.8 which doesn't have `GTestConfig.cmake`
* By explicitly specify config mode in `find_package(GTest REQUIRED CONFIG)`, you can use
    - `GTest::gtest` and `GTest::gmock` targets

## gtest_add_tests()
This function scans the source files to identify tests
* Effective in cross-compiling environments
* Makes setting additional properties on tests more convenient
* However, its handling of parameterized tests is _less comprehensive_, and it requires _re-running_ CMake to detect changes to the list of tests.

## gtest_discover_tests()
Introduced in CMake 3.10, this function discovers tests by asking the compiled test executable to enumerate its tests
* More robust and provides better handling of parameterized tests
* Don't require re-running
* It may not work in a cross-compiling environment
* Setting test properties is less convenient.

## Reference
[Quickstart: Building with CMake | GoogleTest](https://google.github.io/googletest/quickstart-cmake.html)
