# Ranger Terminal File Manager

## Key Shortcuts
* `r` open_with
* `zh` | `<C-h>` show hidden file
* `s` shell command
* `S` quit in current folder
* navigation
    * `[` & `]` navigation between parent folder
    * `H` & `L` navigation in history
    * `J` & `<C-d>` move down half page
    * `K` & `<C-u>` move up half page
* find
    * `/` & `n` & `N` search/jump
    * `f` fast find and open
    * `zf` filter(only show matched terms)
    * `<C-f>` find with fzf
* `g` jumps
    * `gh` goto home folder
    * `gr` goto to root folder
    * `gv` goto vimrc folder
    * `gi` goto github repository folder
    * `gj` autojump, use `<Tab>` for completion
    * `gp` goto project folder
* `y` copy
    * `yy`
    * `yp` copy full file path
    * `yn` copy file name
    * `yd` copy directory path
    * `y`. yank file name without extension
* `p` paste
    * `pp` normal paste
    * `po` paste and overwrite
* rename
    * `cw` rename totally
    * `a` rename at end of the filename, before suffix
    * `i` rename at begin of the filename
    * `A` rename at end of the filename
* `d` cut
    * `dd` normal cut
    * `dD` totally delete
    * `du` similar as `du` command in shell
    * `dU` du and sort
* `o` sorting
    * `os` sort by size
    * `on` sort by name
    * `oc` sort by ctime
    * `om` sort by mtime
* `w` task view
    * `dd` cancel task
* marking
    * `<Space>` toggle marking file
    * `*` toggle marking file
    * `v` mark all files
    * `uv` unmark all files
    * `V` toggle visual mode
    * `uV` toggle reverse visual mode
* file operation
    * `=` chmod
    * `bf` create file (nvim)
    * `bd` create directory (mkcd)
    * `C` compress files
    * `X` extract here
* others
    * `bg` change background wallpaper with High Ubunterra
