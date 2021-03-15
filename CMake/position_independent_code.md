# Position Independent Code

* The `POSITION_INDEPENDENT_CODE` property determines whether position independent executables or shared libraries will be created
* This property is `True` by default for `SHARED` and `MODULE` library targets
* This property is initialized by a global variable `CMAKE_POSITION_INDEPENDENT_CODE` if it is set
* `set_target_properties(<target_name> PROPERTIES POSITION_INDEPENDENT_CODE ON)`

**Caveats**:
When linking `OBJECT` / `STATIC` targets into a `SHARED` target, those targets should be compiled with `-fPIC`

## Reference
[c++ - Combining CMake object libraries with shared libraries - Stack Overflow](https://stackoverflow.com/questions/50600708/combining-cmake-object-libraries-with-shared-libraries)
