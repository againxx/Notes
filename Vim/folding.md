# Folding

## Folding methods

详见`h: fold-methods`

method | description
:-|:-
manual | 手动定义折叠
__indent__ | 根据缩进定义折叠等级，适合Python
__expr__ | 通过表达式定义折叠，配合插件使用（如：vim-markdown）
syntax | 根据语法高亮折叠
diff | folds for unchanged text
marker | 通过markers折叠

## Folding commands

| command | effect                                                              |
|:-------:|:--------------------------------------------------------------------|
|   `zi`  | switch folding on or off (整体开关折叠功能)                         |
|   `za`  | toggle current fold open/closed (仅开关当前折叠)                    |
|   `z;`  | toggle current fold open/closed (自定义)                            |
|   `zo`  | open current fold                                                   |
|   `zO`  | recursively open current fold                                       |
|   `zc`  | close current fold (如果当前折叠已经关闭，则会进一步关闭上一级折叠) |
|   `zC`  | recursively close current fold                                      |
|   `zR`  | open all folds                                                      |
|   `zM`  | close all folds                                                     |
|   `zv`  | expand folds to reveal cursor (zMzv仅展开当前光标处的折叠)          |
|   `zj`  | move down to top of next fold                                       |
|   `zk`  | move up to bottom of previous fold                                  |
|   `[z`  | Move to the start of the current open fold                          |
|   `]z`  | Move to the end of the current open fold                            |

## Folding level

* 1全折叠, 99不折叠
* `zm`减小1, `zr`增加1
* `set foldlevelstart=99`设置初始不折叠
* `:set foldlevel?`或者`:echo &foldlevel`查看当前foldlevel
