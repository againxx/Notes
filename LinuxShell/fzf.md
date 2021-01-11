# FZF

## Keybindings
* `ctrl-r` search back command history
* `ctrl-t` fuzzy find through current directory
* `alt-c` cd into selected directory
* `<tab>` select multiple files
* `**<tab>` autocompletion for other command's arguments (find files or directories)

## Search Syntax
* type in multiple search terms delimited by **spaces**
* a single `|` acts as OR operator
    - to match entries start with `core` and end with either `go`, `rb`, or `py`, `^core go$ | rb$ | py$`

| Token     | Match type                 | Description                          |
|-----------|----------------------------|--------------------------------------|
| `sbtrkt`  | fuzzy-match                | Items that match `sbtrkt`            |
| `'wild`   | exact-match (quoted)       | Items that include `wild`            |
| `^music`  | prefix-exact-match         | Items that start with `music`        |
| `.mp3$`   | suffix-exact-match         | Items that end with `.mp3`           |
| `!fire`   | inverse-exact-match        | Items that do not include `fire`     |
| `!^music` | inverse-prefix-exact-match | Items that do not start with `music` |
| `!.mp3$`  | inverse-suffix-exact-match | Items that do not end with `.mp3`    |

## Miscellanies
* use `fd` as fzf default find command to get rid of files ignored by git

## Examples
* `kill -9 <tab>` completion for PIDs
* `ssh **<tab>` / `telnet **<tab>` completion for host names
* `unset **<tab>` / `export **<tab>` / `unalias **<tab>` environment variables / aliases
