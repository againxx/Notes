# Buffer Protocol

* Python objects that manage an underlying memory can be accessed directly without intermediate copy via **Buffer Protocol**
* Builtin types that implement buffer protocol
    - bytes, bytearray
    - array.array
* Third party libraries' types
    - numpy.ndarray
* The protocol has two sides:
    - on the producer side, a type can export a _buffer interface_ which allows objects of that type to expose information about their underlying buffer.
    - on the consumer side, several means are available to obtain a pointer to the raw underlying data of an object.
* The buffer interface allows objects to selectively export read-write or read-only buffers
