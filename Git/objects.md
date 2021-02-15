# Git Objects

There are four types of objects in git, git stores snapshots instead of differences
* blob: used to store file data - it's generally a file
* tree: basically like a directory - it references a bunch of other blobs and trees
* commit: points to a singel tree - it marks what the project looked like at a certain time point
* tag: marks a special commit

## Blob Object
Blob is a chunk of binary data, it doesn't have any attributes even a file name
![blob object](https://gitee.com/againxx/image-storage/raw/master/images/object-blob.png =300x)

* `git show <SHA1> / git cat-file -p <SHA1>` to examine its contents

## Tree Object
![tree object](https://gitee.com/againxx/image-storage/raw/master/images/object-tree.png =300x)
* `git show <SHA1>`
* `git ls-tree <SHA1>` include SHA1 code for every object referenced by the tree

## Commit Object
![commit object](https://gitee.com/againxx/image-storage/raw/master/images/object-commit.png =300x)

## Tag Object
![tag object](https://gitee.com/againxx/image-storage/raw/master/images/object-tag.png =300x)
