# Redirection input and output

重定向主要操作三种文件以及其对应的文件描述符(file descriptor)

file | file descriptor | redirection
:-|:-|:-
stdin | 0 | `<` / `0<`
stdout | 1 | `>` / `1>`
stderr | 2 | `2>`

---------

`&>`同时重定向stdout和stderr，等同于`> file 2>&1`  
注：`>&`不同于`&>`，前者表示将左边描述符变为右边描述符的复制  
所以得先将stdout重定向到file，再将stderr复制为stdout才有意义，要是使用`2>&1 > file`则stderr变为原先的stdout，stdout单独重定向为file

---------
Appending模式（不覆盖文件中已有内容）
* `>>` stdout附加重定向
* `2>>` stderr附加重定向
* `&>>` stdout和stderr同时附加重定向
