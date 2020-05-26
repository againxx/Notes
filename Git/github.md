# Github
Two collaborative development models:
* Fork and pull model
* Shared repository model

[Github Flow](https://guides.github.com/introduction/flow/)

## Fork and pull
Fork an existing repository and push changes to their personal fork.
You do not need permission to the source repository to push to a user-owned fork.
The changes can be pulled into the source repository by the project maintainer.

Useful Command:
* `git remote add upstream <source repository>` 除origin remote仓库外，可以额外添加source仓库，来跟进原版仓库的进度

## Shared repository
Collaborators are granted push access to a single shared repository and topic branches are created when changes need to be made.
Pull requests are useful in this model as they initiate code review and general discussion about a set of changes
before the changes are merged into the main development branch. CI (continuous integration) system can also be used in pull requests.
