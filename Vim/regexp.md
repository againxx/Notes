# Vim Regular Expression

## Multi Items
|              |                     |
|--------------|---------------------|
| `*`          | 0或多个, 贪婪匹配   |
| `\+`         | 1或多个, 贪婪匹配   |
| `\{-}`       | 0或多个, 非贪婪匹配 |
| `\?` 或 `\=` | 0或1个, 贪婪匹配    |
| `\{n,m}`     | n~m个, 贪婪匹配     |
| `\{-n,m}`    | n~m个, 非贪婪匹配   |

## Ordinary Atoms
|       |                                                     |
|-------|-----------------------------------------------------|
| `\<`  | 单词开头                                            |
| `\>`  | 单词结尾                                            |
| `.`   | 任意字符, 不包括行尾                                |
| `\_.` | 任意字符, 包含行尾 (换行符算一个字符, 可以跨行搜索) |

## Character Classes
|      |                                             |
|------|---------------------------------------------|
| `\k` | keyword character                           |
| `\K` | like `\k`, but excluding digits             |
| `\w` | word character: [0-9A-Za-z_]                |
| `\W` | non-word character: [^0-9A-Za-z_]           |
| `\s` | whitespace character: \<Space\> and \<Tab\> |
| `\S` | non-whitespace character                    |
| `\d` | digit: [0-9]                                |
| `\D` | non-digit: [^0-9]                           |
