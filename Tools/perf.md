# Perf

## Common Commands
* `perf stat -e <event1>,<event2>... <program>`

## Software Events
* `cpu-clock` uses the Linux CPU clock as the timing source to measure the passage of time

## Hardware Events
Hardware events directly read the count in PMU(Performance Monitor Unit)

| Event Name          | Description                                                |
|---------------------|------------------------------------------------------------|
| cpu-cycles / cycles | cpu cycle num                                              |
| instructions        | instruction architecturally executed (retired instruction) |
| cache-references    |                                                            |

For some hardware events that do not have symbolic names in perf, you can use its raw identifier such as `r008`

Performance counters (usually) support two usage modes: counting and sampling
* Counting mode: the counters are configured and the number of events is read and reported
    - with lower overhead
    - can only measure the events of application as a whole
    - mainly used by `perf stat`
* Sampling mode: they are configured to generate a sampling interrupt after a certain number of events are counted
    - imposes additional overhead
    - can issue to specific region of code
    - mainly used by `perf record`

## Utils Commands
* `perf evlist -F` 可以列出perf.data中sample的event和频率

## Reference
[PERF | Sand, software and sound](http://sandsoftwaresound.net/perf/)
