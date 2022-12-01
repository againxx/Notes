# Awk

## Structure of Awk program
```awk
pattern { action }
```
* Awk scans a sequence of input lines one after another searching for lines that are matched
* Every input line is tested against each pattern in turn
* For each match, the `{action}` is executed
* After every applicable `{action}` is executed, the next line is processed
* Action are enclosed in braces to distinguish them from the pattern

* Either the pattern or the action can be omitted
    - The default pattern matches _every line_
    - The default action is _print the whole line_

## Awk patterns
* Awk patterns are basically just "if" statements
* Summary of patterns
    - `BEGIN { statements }` the statements are executed once **before** any input has been read
    - `END { statements }` the statements are executed once **after** all input has been read
    - `expression { statements }` the statements are executed at each input line where the expression is true (nonzero or non-null)
    - `/regular expression/ { statements }` the statements are executed at each input line that contains a string matched by the regular expression
        - `/regular/` implies "$0 ~"
    - `compound pattern { statements }` a compound pattern combines expression with `&&`, `||`, `!`, and parentheses
    - `pattern1, pattern2, { statements }` **a range pattern** matches each input line from a line matched by _pattern1_ to the next line matched by _pattern2_, inclusive;
    the statements are executed at each matching line.

## Awk actions
* Parentheses in function calls are optional
* Can override fields or create new fields
* The default argument for many functions is $0

## Special variables
| Variable | Meaning                                      | Default |
|----------|----------------------------------------------|---------|
| NF       | num of fields in current record              | N/A     |
| NR       | num of records read so far                   | N/A     |
| ARGC     | num of command-line arguments                | N/A     |
| ARGV     | array of command-line arguments              | N/A     |
| FILENAME | name of current input file                   | N/A     |
| FNR      | record number in current file                | N/A     |
| FS       | controls the input field separator           | " "     |
| RS       | controls the input record separator          | "\n"    |
| OFMT     | output format for numbers                    | "%.6g"  |
| OFS      | output field separator                       | " "     |
| ORS      | output record separator                      | "\n"    |
| RLENGTH  | length of string matched by _match_ function | N/A     |
| RSTART   | start of string matched by _match_ function  | N/A     |
| SUBSEP   | subscript separator                          | "\034"  |
