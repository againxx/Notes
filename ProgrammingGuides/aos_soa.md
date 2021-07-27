# AoS vs SoA

`AoS` = Array of structures
`SoA` = Structure of arrays

These are two ways of arranging a sequence of records in memory

## Structure of Arrays
SoA **separates** elements of structure into parallel array per fields, which reflects the concept of data oriented programming

```c
struct pointlist3D {
    float x[N];
    float y[N];
    float z[N];
};
struct pointlist3D points;
float get_point_x(int i) { return points.x[i]; }
```

### Pros & Cons
#### Pros
* Easier manipulation with packed SIMD instructions
* If only a specific part of the record is needed, only those parts need to be iterated over, allowing more data to fit onto a single cache line.

#### Cons
* Requires more cache ways when traverse data
* Inefficient indexed addressing (the record is not contiguous)

## Array of Structures
* More natural and object-oriented way
```c
struct point3D {
    float x;
    float y;
    float z;
};
struct point3D points[N];
float get_point_x(int i) { return points[i].x; }
```

## Reference
[AoS and SoA - Wikipedia](https://en.wikipedia.org/wiki/AoS_and_SoA)
