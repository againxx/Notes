# Zotero

## 条目管理
### 新建条目
* Zotero Connector网页抓取
* 拖拽本地文档到Zotero中
* 手动创建新条目
* 索引码创建新条目(ISBN, DOI)

### 删除条目
* 右键删除条目, 会将所有条目的删除
* 一般选择从分类中移除条目

## Tags
* 标签可以指定颜色和位置
* 指定位置后, 可通过1~9来快速添加或删除标签

## Plugins
### Zotero Connector
Zotero Connector直接剪藏到本地Zotero客户端, 会自动下载pdf文件, 但是可能需要等一会儿

### ZotFile
#### 功能一: 目录检测
对于一些无法通过Zotero Connector自动下载的文档, 可以手动下载到ZotFile监控的目录, 然后在Zotero的条目下右键选择Attach New File

#### 功能二: 发送附件到指定目录并收回
* 方便将文档发送到移动端阅读, 并在阅读后收回. Tablet Files 分类下就是我们发送的条目, 而 Tablet Files (modified) 下是在移动端阅读并修改过的文档的条目.
* 需要指定一个特殊目录: 网盘自动同步目录, 移动端修改自动同步目录的内容后, 可以在Zotero中将其收回, 则移动端的批注即可同步到PC端

#### 功能三: 自动提取pdf批注
在PDF中标注好批注后, 可以通过右键->Manage Attachments->Extract Annotations来自动提取所作标注作为notes

#### 功能四: 重建文件目录 (不推荐)
1. 理由一: 不必要, 用Zotero管理即可
2. 理由二: 对Zotero服务器的偏好
3. 理由三: 对于需要批量将论文发给别人时, 可以考虑使用群组功能, 或者复制条目地址, 然后用shell脚本操作

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

### Zutilo
* 为Zotero右键菜单中, 添加了条目管理相关的菜单(标签复制, 粘贴, 文档关联等)
* 允许为Zotero的很多功能设置快捷键

[shortcuts](#shortcuts)

### Zotero-Better-BibTex
方便设置citation key和.bib文件

### Zotcite
Vim插件, 可以在markdown中引用Zotero的文献

## Add Reference
### Word
使用Zotero针对Word的插件

### Latex
使用Better BibTex

### Markdown
实用Markdown写论文的优点:
1. Markdown vs. Word
    - 减少格式干扰
    - 专注文本本身
2. Markdown vs. Latex
    - 更简单
    - 更轻量
3. Markdown据有文档管理功能 (主要指一些笔记软件)
    - 实现文档all-in-one

## Shortcuts

| Keybinding     | Description            |
|:--------------:|:----------------------:|
| `Ctrl-s`       | 开关条目属性窗口       |
| `Ctrl-e`       | 开关分类窗口           |
| `Ctrl-h`       | 聚焦分类窗口           |
| `Ctrl-l`       | 聚焦条目窗口           |
| `Ctrl-Shift-k` | 快速查找               |
| `Ctrl-f`       | 快速查找               |
| `Ctrl-i`       | 编辑条目信息           |
| `Ctrl-n`       | 添加条目笔记           |
| `Ctrl-t`       | 添加条目标签           |
| `Ctrl-r`       | 添加关联文献           |
| `Ctrl-Shift-t` | 开关标签选择器         |
| `Alt-r`        | 关联条目               |
| `Ctrl-o`       | 打开附件文件位置       |
| `Ctrl-d`       | 删除条目标签           |
| `Ctrl-y`       | 复制条目标签           |
| `Ctrl-p`       | 粘贴条目标签           |
| `Ctrl-/`       | 聚焦标签搜索框         |
| `-`            | 折叠文库, 或条目附件   |
| `+`            | 展开文库, 或条目附件   |
| `Alt`          | 高亮所选条目的所在分类 |
| `Shift`        | 移动所选条目而不是复制 |

## Other
* 与他人合作, 可以采用群组功能
* 工具->创建时间轴, 可以按下载、修改或者发表的时间展示文档
