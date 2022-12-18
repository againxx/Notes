# Ld
* GUN ld is infamous for the unreasonable requirement of specifying libraries in the order of reverse dependence
    - an object's dependencies follow the object or library
    - It's very annoying once we have to deal with circular dependencies, and will have to specify the library _again_
* As a solution, we can define a group of archives:
> --start-group archives --end-group
> The archives should be a list of archive files. They may be either explicit file names of -l options
Or the short-hand version:
> -( archives -)

* This causes the linker to perform an exhaustive search through all the libs in the group until all symbols are resolved,
which may have a possible performance impact.

## gold
* An alternative linker _gold_  has a `--gdb-index` option to build the gdb index at link time
