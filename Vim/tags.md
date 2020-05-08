# Tags

use exuberant ctags to generate tag files `ctags -R`, which will generate a `tags` file in current directory

use `set tags=tags;` to use the generated tag file

* `<C-]>` go to the definition the tag
* `<C-t>` go back to previous position
* `:tn` next tag (switch between tags of the same name)
* `:tp` previous tag
* `:ts` open a tag list to select
* `g]` like `<C-]>`, but open a tag list for select

