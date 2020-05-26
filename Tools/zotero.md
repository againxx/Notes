# Zotero

## Plugins
### Zotero Connector
Zotero Connector直接剪藏到本地Zotero客户端, 会自动下载pdf文件, 但是可能需要等一会儿

### ZotFile
#### 功能一: 目录检测
对于一些无法通过Zotero Connector自动下载的文档, 可以手动下载到ZotFile监控的目录, 然后在Zotero的条目下右键选择Attach New File
#### 功能二: 发送附件到指定目录并收回
* 方便将文档发送到移动端阅读, 并在阅读后收回. Tablet Files 分类下就是我们发送的条目, 而 Tablet Files (modified) 下是在移动端阅读并修改过的文档的条目.
* 需要指定一个特殊目录: 网盘自动同步目录, 移动端修改自动同步目录的内容后, 可以在Zotero中将其收回, 则移动端的批注即可同步到PC端

### ZoteroQuickLook
[Github Page](https://github.com/mronkko/ZoteroQuickLook)

Use gnome-sushi instead of gloobus-preview to preview pdf:
1. `sudo apt install gnome-sushi`
2. make a shell script with following content
```shell
#!/bin/bash
# run GNOME sushi to preview pdf in zotero

PDF_FILE=$(/usr/bin/realpath "$*")

dbus-send --print-reply --dest=org.gnome.NautilusPreviewer /org/gnome/NautilusPreviewer org.gnome.NautilusPreviewer.ShowFile string:"file://$PDF_FILE" int32:0 boolean:false
```
3. make the script executable and create a symbolic link to `/usr/bin/gloobus-preview`
