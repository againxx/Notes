# Debug

## CMakePrintHelpers
```cmake
include(CMakePrintHelpers)
# Prints the values of the properties of the given targets, source files, directories, tests or cache entries
# Exactly one of the scope keywords must be used
cmake_print_properties([TARGETS target1 ..  targetN]
                      [SOURCES source1 .. sourceN]
                      [DIRECTORIES dir1 .. dirN]
                      [TESTS test1 .. testN]
                      [CACHE_ENTRIES entry1 .. entryN]
                      PROPERTIES prop1 .. propN )
cmake_print_variables(var1 var2 ..  varN)
```
