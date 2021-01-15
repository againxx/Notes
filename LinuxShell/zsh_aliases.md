# Zsh Aliases

## Simple Aliases
```shell
alias <my-alias>="<command>"
```

## Suffix Aliases
```shell
alias -s <extension>=<name-of-the-tool>

# JSON files
alias -s json=code

# bulk association
alias -s {cs,ts,html}=code
```

## Functions for Aliases with Parameters
```shell
aliasname() {
  command $1 $2
}
```

## Global Aliases
A global alias is aggressive. Once registered, it replaces all occurrences of the alias name with the specified command.
```shell
alias -g <my-alias>="<command>"
```

## Operating System Specific Aliases
```shell
# macOS aliasses
if [[ $OSTYPE == darwin* ]]; then
alias flush='dscacheutil -flushcache'
# Apps
alias browse="open -a /Applications/Google\ Chrome.app"
# * Browse Azure Portal
alias azure="browse https://preview.portal.azure.com"
fi
```

## Reference
[5 Types Of ZSH Aliases You Should Know](https://thorsten-hans.com/5-types-of-zsh-aliases)
