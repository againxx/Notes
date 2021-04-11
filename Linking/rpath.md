# RPATH

* RPATH designates run-time search path hard-coded in an executable or library file
* Dynamic linking **loaders** use the rpath to find required libraries
* A path to the shared libraries will be encoded into the header of the executable if rpath is set, overriding or supplementing the system default search paths

## Why shoud we set RPATH
* Setting `RPATH` is useful for *private libraries* - libraries that are shared only among a small number of executables coming from the same package
* Installing *private libraries* in the same path as the general libraries will causes two problems
    - The build-time linker will still find them during link time (maybe some special version of the library that you only use in particular project)
    - It increases the number of files present in the single directory thus slowing down its content accessing
* Setting `RPATH` can change the library search path so that one executable or library is able to link the desired dependency during rum-time.

## How to check the value of RPATH
* `objdump -p <path/to/executable> | grep RPATH`
* `readelf -d <path/to/executable> | head -20`
* `chrpath -l <path/to/executable>` (a tool to edit the rpath)

`$ORIGIN` is a special variable that indicate actual executable file name.
It is resolved to where the executable is at run-time, and can be quiet useful when setting `RPATH`

Note that, on Windows, the same `PATH` variable that is used to find the commands is used to load the libraries;
And the libraries are looked for in the same directory where the executable is first of all.
(No need for $ORIGIN, but is there the concept of RPATH in Windows?)

## How to set RPATH
### During compilation
* `gcc -Wl,-rpath <path/to/libraries>` -rpath is the option of `ld` not `gcc`, so we need to use `-Wl,` to specify it

**Note:**
* Using `gcc -L <path/to/libraries>` only let the linker add dependency successfully, but it will not add the specified path into `rpath`
* By using `ldd`, the dependent libraries will be marked `not found`

### After compilation
* `chrpath -r ` this command could fail if no rpath was set previously
* `patchelf --set-rpath ‘$ORIGIN/path/to/library’ <executable>`

## RUNPATH
The only difference between `RPATH` and `RUNPATH` is the order they are searched in. Specifically, their relation to `LD_LIBRARY_PATH` 
* `RPATH` is searched in before `LD_LIBRARY_PATH` while `RUNPATH` is searched in after.
* The meaning of this is that `RPATH` cannot be changed dynamically with environment variables while `RUNPATH` can

## Reference
* [Creating relocatable Linux executables by setting RPATH with $ORIGIN | by Luke Chen | Medium](https://nehckl0.medium.com/creating-relocatable-linux-executables-by-setting-rpath-with-origin-45de573a2e98)
