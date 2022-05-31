# Tag

## Questions
* What are the lightweight tags and how to create them?

## Create tag
* `git tag <tag_name>` create a normal tag
* `git tag -a <tag_name> -m "<message>"` create an annotated tag
* `git tag <tag_name> <commit_hash>` create a tag from past commit

## List tag
* `git tag` list all tags
* `git show <tag_name>` show detail information about a tag
* `git tag -l "<wildcards>"` 可以使用通配符来列出匹配的tag

## Delete tag
* `git tag -d <tag_names> / git tag --delete <tag_names>` delete one or multiple tag

## Push tag to remote
* push到github上的tag会自动形成一个release (to be verified)
* `git push origin <tag_name>`
* Push all tags to the remote
    - `git push --tags`
    - `git push origin --tags`
* To delete tag from remote
    - `git push origin -d <tag_names>`
    - `git push origin --delete <tag_names>`
    - `git push origin :<tag_name>`

## Fetch tag from remote
* `git fetch --tags`

## Checkout to tag
* Cannot directly checkout to a tag (use SHA1 hash reference instead), it actually can !!
* But can create a branch from a tag and checkout to that branch
    * `git checkout -b <branch_name> <tag_name>`
