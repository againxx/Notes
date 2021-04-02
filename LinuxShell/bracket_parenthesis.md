# Bracket & Parenthesis in Bash

## Single Square Bracket
* Same as `test` command without `$`
* When used with `$[ ]`, it can perform some basic integer arithmetic wihout escape `*`, `<` ...

### Caveats
* `<` and `>` are viewed as redirection operators

## Double Square Bracket
Extended test has following advantages

1. don't need to escape `<` and `>`
```sh
[ "abc" /> "abd" ] && echo Yes || echo No
[[ "abc" > "abd" ]] && echo Yes || echo No
# No
```

2. can use `==` for string and number comparison
```sh
var=1
[[ $var == 1 ]] && echo Yes || echo No
# Yes
```

3. can use wildcards and regular expressions
    - 注意通配符不能用引号扩起来, 否则就变成了普通字符
```sh
[[ "string" == str* ]] && echo Yes || echo No
[[ "string" =~ "\wtr.*" ]] && echo Yes || echo No
```

## Single Curly Bracket
## Double Curly Bracket
## Single Parenthesis
## Double Parenthesis
