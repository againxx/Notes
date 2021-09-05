# Quoting

* Quoted items can be concatenated with nonquoted items as well as with other quoted items. The shell turns everything into one argument.
* Preceding any single character with a backslash ('\') quotes that character. The shell removes the backslash and passes the quoted character on to the command.
* Single quotes protect everything between the opening and closing quotes. It's _impossible_ to embed a single quote inside single-quoted text.
* Double quotes protect most things between the opening and closing quotes. The shell does at least variable and command substitution.
    - `$`, `` ` ``, ` \ `, and `"` need to be escaped
* Null strings are removed when they occur as part of a non-null command-line argument, while explicit null objects are kept
    - `awk -F "" 'program' files` is correct, while
    - `awk -F"" 'program' files` is wrong

## Tricks
* Mixing single and double quotes is difficult, we can resort to quoting concatenation
```shell
$ awk 'BEGIN { print "Here is a single quote <'"'"'>" }'
Here is a single quote <'>
# or
$ awk 'BEGIN { print "Here is a single quote <'\''>" }'
# or
$ awk "BEGIN { print \"Here is a single quote <'>\" }"
# or
$ awk 'BEGIN { print "Here is a single quote <\47>" }'
```
