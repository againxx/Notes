# FetchContent
This module enables populating content at **configure time** via any method supported by the `ExternalProject` module
* Difference between `ExternalProject`
    - `ExternalProject_Add()` downloads at build time
    - `FetchContent` makes the content available immediately, which can be used then in `add_subdirectory()` / `include()` / `file()`

There are two steps to populate the content
* Define content population details, `FetchContent_Declare()`
* Perform the actual population, `FetchContent_MakeAvailable()`
