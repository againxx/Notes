# Tag

## Create tag
* `git tag <tag_name>` 创建一个普通的tag
* `git tag -a <tag_name> -m "<message>"` 创建一个带注解的tag
* `git tag <tag_name> <commit_hash>` create a tag from past commit

## List tag
* `git tag` 列出所有的tag
* `git show <tag_name>` 显示一个tag的详细信息
* `git tag -l "<wildcards>"` 可以使用通配符来列出匹配的tag

## Delete tag
* `git tag -d <tag_names> / git tag --delete <tag_names>` 删除一个或多个tag

## Push tag to remote
* push到github上的tag会自动形成一个release (待验证)
* `git push origin <tag_name>`
* Push all tags to the remote
    - `git push --tags`
    - `git push origin --tags`
* To delete tag from remote
    - `git push origin -d <tag_names>`
    - `git push origin --delete <tag_names>`
    - `git push origin :<tag_name>`

## Checkout to tag
* Cannot directly checkout to a tag (use SHA1 hash reference instead)
* But can create a branch from a tag and checkout to that branch
    * `git checkout -b <branch_name> <tag_name>`
