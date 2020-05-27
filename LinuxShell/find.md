# Find

`find <directory> [<tests>] [<options>] [<actions>]`

## Tests
### Name Test
`-name <pattern>`

### Type Test
`-type <file_type>`
| File Type | Description                   |
|-----------|-------------------------------|
| d         | Directory                     |
| f         | Regular file                  |
| l         | Symbolic link                 |
| b         | Block special device file     |
| c         | Character special device file |

注:
* block device: 以块为单位进行读取, 类似普通文件, 比如/dev/sda
* character device: 以字符为单位进行处理, 类似管道或者串口, 比如/dev/tty

### Size Test
## Options

## Actions
