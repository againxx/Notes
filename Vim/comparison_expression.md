# Comparison Expression

| use                   | 'ignorecase' | match case | ignore case |
|:----------------------|:------------:|:----------:|:-----------:|
| equal                 |      ==      |     ==#    |     ==?     |
| not equal             |      !=      |     !=#    |     !=?     |
| greater than          |       >      |     >#     |      >?     |
| greater than or equal |      >=      |     >=#    |     >=?     |
| smaller than          |       <      |     <#     |      <?     |
| smaller than or equal |      <=      |     <=#    |     <=?     |
| regexp matches        |      =~      |     =~#    |     =~?     |
| regexp doesn't match  |      !~      |     !~#    |     !~?     |
| same instance         |      is      |     is#    |     is?     |
| different instance    |     isnot    |   isnot#   |    isnot?   |

Examples:  
* "abc" ==# "Abc"	  evaluates to 0
* "abc" ==? "Abc"	  evaluates to 1
* "abc" == "Abc"	  evaluates to 1 if 'ignorecase' is set, 0 otherwise
