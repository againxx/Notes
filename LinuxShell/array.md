# Array

```bash
os=("ubuntu" "windows" "kali")

# expand all elements
echo "${os[@]}"
# first element
echo "${os[0]}"
# indexes of the array
echo "${!os[@]}"
# length
echo "${#os[@]}"
# append element (can be at any index)
os[3]="mac"
# remove element
unset os[2]
```
