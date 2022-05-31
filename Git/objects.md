# Git Objects

There are four types of objects in git, git stores *snapshots* instead of *differences*
* blob: used to store file data - it's generally a file
* tree: basically like a directory - it references a bunch of other blobs and trees
* commit: points to a single tree - it marks what the project looked like at a certain time point
* tag: marks a special commit

## Blob Object
* Blob is a chunk of binary data, it doesn't have any attributes even a file name
* Two files have the same contents will share the same blob object (this reduces the redundancy of the same files between different commits)
![blob object](http://images.againxx.cn/object-blob.png =300x)

* `git show <SHA1> / git cat-file -p <SHA1>` to examine its contents

## Tree Object
* A tree is a simple object that has a bunch of pointers to blobs and other trees, which represents the content of a directory or subdirectory
![tree object](http://images.againxx.cn/object-tree.png =300x)

* `git show <SHA1>` list only file / directory names
* `git ls-tree <SHA1>` include SHA1 code and permission mode for every object referenced by the tree
* `git cat-file -p <SHA1>` same as `ls-tree`

```shell
$ git ls-tree fb3a8bdd0ce
100644 blob 63c918c667fa005ff12ad89437f2fdc80926e21c    .gitignore
100644 blob 5529b198e8d14decbe4ad99db3f7fb632de0439d    .mailmap
100644 blob 6ff87c4664981e4397625791c8ea3bbb5f2279a3    COPYING
040000 tree 2fb783e477100ce076f6bf57e4a6f026013dc745    Documentation
100755 blob 3c0032cec592a765692234f1cba47dfdcc3a9200    GIT-VERSION-GEN
100644 blob 289b046a443c0647624607d471289b2c7dcd470b    INSTALL
100644 blob 4eb463797adc693dc168b926b6932ff53f17d0b1    Makefile
100644 blob 548142c327a6790ff8821d67c2ee1eff7a656b52    README
...
```

**Note** that the files all have mode 644 or 755: git actually only pays heed to the executable bit

## Commit Object
* The commit object links a physical state of a tree with a description of how we got there and why
![commit object](http://images.againxx.cn/object-commit.png =300x)

* `git cat-file -p <SHA1>` without commit object SHA1
* `git show -s --pretty=raw <SHA1>`
```shell
$ git show -s --pretty=raw 2be7fcb476
commit 2be7fcb4764f2dbcee52635b91fedb1b3dcf7ab4
tree fb3a8bdd0ceddd019615af4d57a53f43d8cee2bf
parent 257a84d9d02e90447b149af58b271c19405edb6a
author Dave Watson <dwatson@mimvista.com> 1187576872 -0400
committer Junio C Hamano <gitster@pobox.com> 1187591163 -0700

    Fix misspelling of 'suppress' in docs

    Signed-off-by: Junio C Hamano <gitster@pobox.com>
```

## Tag Object
![tag object](http://images.againxx.cn/object-tag.png =300x)
* Tag object can be viewed using `git cat-file tag <tag_name>`
* `git tag` can also be used to create "lightweight tags", which are not tag objects at all, but just simple references whose names begin with "refs/tags/"

## Example
```shell
$>tree
.
|-- README
`-- lib
    |-- inc
    |   `-- tricks.rb
    `-- mylib.rb

2 directories, 3 files
```
![objects example](http://images.againxx.cn/objects-example.png =750x)

## Reference
[Git Book - The Git Object Model](https://shafiul.github.io//gitbook/1_the_git_object_model.html)
