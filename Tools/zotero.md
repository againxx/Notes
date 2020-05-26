# Zotero

## Plugins
### ZoteroQuickLook
[Github Page](https://github.com/mronkko/ZoteroQuickLook)

Use gnome-sushi instead of gloobus-preview to preview pdf:
1. `sudo apt install gnome-sushi`
2. make a shell script with following content
```shell
#!/bin/bash
# run GNOME sushi

PDF_FILE=$(/usr/bin/realpath "$*")
echo "$PDF_FILE" > test.txt

dbus-send --print-reply --dest=org.gnome.NautilusPreviewer /org/gnome/NautilusPreviewer org.gnome.NautilusPreviewer.ShowFile string:"file://$PDF_FILE" int32:0 boolean:false
```
3. make the script executable and create a symbolic link to `/usr/bin/gloobus-preview`
