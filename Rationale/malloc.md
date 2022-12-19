# Malloc Internals

## Overview
* glibc *malloc* is a "heap" style malloc, which means chunks of various sizes exist within a larger region of memory (a "heap")
* Another implementation uses bitmaps and arrays, or region of same-sized blocks

### Common terms
* **Arena**: A structure that is shared among one or more threads which contains references to one or more heaps
as well as linked lists of chunks within those heaps which are "free". Threads assigned to each arena will allocate
memory from that arena's free lists.
* **Heap**: A contiguous region of memory that is subdivided into chunks to be allocated. Each heap belongs to exactly one arena
* **Chunk**: A small range of memory that can be allocated (owned by the application), freed (owned by glibc), ore combined
with adjacent chunks into larger ranges. Note that a chunk is a **wrapper** around the block of memory that is given to
the application. Each chunk exists in one heap and belongs to one arena.
* **Memory**: A portion of the application's address space which is typically backed by **RAM** or **swap**

## What is a Chunk?
* Glibc's malloc is chunk-oriented. It divides a large region of memory (a "heap") into chunks of various sizes.
* Each chunk includes meta-data about how big it is (via a `size` field)
* Within the malloc library, a "chunk pointer" or `mchunkptr` does not point to the beginning of the chunk, but
to the last word in the previous chunk - i.e. the first field in `mchunkptr` is not valid unless you know the
previous chunk is free

## Reference
[glibc wiki MallocInternals](https://sourceware.org/glibc/wiki/MallocInternals)
