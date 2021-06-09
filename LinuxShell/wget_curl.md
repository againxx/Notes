# wget & curl

## wget 下载器
**`wget [option] [URL]`**  
使用`--`结束option部分,例如`wget -o log -- -x`中的`-x`为URL

| options                  | description                                                     |
|:-------------------------|:----------------------------------------------------------------|
| `-o <logfile>`           | 记录所有信息到logfile                                           |
| `-O <file>`              | 下载内容重定向到file中，如果使用 - 作为file，则重定向到标准输出 |
| `-i <file>`              | 从file读入URLs                                                  |
| `-c`                     | 继续下载                                                        |
| `-q`                     | 关闭输出                                                        |
| `-t <number>`            | 指定重试次数，默认为20次，0/inf表示无穷次                       |
| `--save-cookies <file>`  | 存储cookies，存储session cookies需要额外指定                    |
| `--keep-session-cookies` | 主要用于登录界面的cookies                                       |
| `--load-cookies <file>`  | 读取存储的cookies文件                                           |

## curl URL工具
**`curl [options] [URL]`**

| options                        | description                                        |
|:-------------------------------|:---------------------------------------------------|
| `-s`                           | silent mode，类似`wget`的`-q`                      |
| `-o <file>`                    | 输出到文件                                         |
| `-O`                           | 输出到和远端同名的文件                             |
| `-L`                           | 跟随重定向                                         |
| `-c -`                         | 继续下载                                           |
| `-x protocol://host:port`      | 使用代理, 注意使用socks5h让socks服务器解析hostname |
| `-d, --data <data>`            | HTTP POST data                                     |
| `-b, --cookie <data/filename>` | Send cookies from string/file                      |
| `-c, --cookie-jar <filename>`  | Write cookies to filename                          |
| `-j, --junk-seesion-cookies`   | Ignore session cookies read from file              |
| `-f, --fail`                   | Fail silently (no output at all) on HTTP errors    |
| `--create-dirs`                | 创建必要的本地文件夹                               |
| `-i`                           | Include the HTTP response headers                  |
