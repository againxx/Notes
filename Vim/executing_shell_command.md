# Executing Shell Command

* `:!{program}`		    execute {program}
* `:r !{program}`		execute {program} and read its output
* `:w !{program}`		execute {program} and send text to its input
* `:[range]!{program}`	filter text through {program}
    - 不带range的时候正常执行program, 带range时, 用program来过滤range内的文本
