# Objcopy
* Use `objcopy --only-keep-debug` and `--add-gnu-debuglink` to split the debug symbols from the binary
* Use the build IDs (GNU ld option `--build-id`) and a network storage to set up a symbol server
