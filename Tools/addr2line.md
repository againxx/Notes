# Addr2line

Given an address in an **executable** or an offset in a section of **relocatable** object -> file name and line number using debugging information

## Options
* `-e` specify the name of executable / relocatable object
* `-f` display function names together with file name and line number
* `-s` display only the base of each file name
* `-j` read offsets relative to the specified section instead of absolute addresses
* `-p` human-friendly output, each location only occupies one line
* `-i` prints back to the first non-inlined function if the address belongs to an inlined function

## Addr2line in Rust
* Rust also has a library and binary utility for translating addresses into function names [addr2line - Rust](https://docs.rs/addr2line/0.15.1/addr2line/)
