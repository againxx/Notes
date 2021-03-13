# Array

## Normal Array
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

## Associative Array
```bash
declare -A ass_arr1
ass_arr1[fruit]=Mango
ass_arr1[bird]=Cockatoo
ass_arr1[flower]=Rose

declare -A ass_arr2=([HDD]=Samsung [Monitor]=Dell [Keyboard]=HHKB)

# go through all keys and print values
for key in "${!ass_arr1[@]}"; do
    echo $key => ${ass_arr1[$key]}
done

# Add new data
ass_arr2+=([Mouse]=Logitech)
```
