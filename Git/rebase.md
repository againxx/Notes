# Rebase

Rebase allows one branch to be relocated farther down the history track.

`git checkout feature-branch` && `git rebase master`

`git pull --rebase` fetch完后调用rebase而不是merge

## Difference between Merging and Rebasing

* Merging will stuff all changes from feature branch into one large merge commit
* Git tree may become complex by using merging

![Merging](https://www.themoderncoder.com/assets/git-merge-graphic.png =750x)

* Rebasing will take all of the commits on feature branch and move them on top of master commits
* Nice clean tree with all your commits laid out nicely in a row

![Rebasing](https://www.themoderncoder.com/assets/git-rebase-graphic.png =750x)

## Rebasing Caveats
It can also be dangerous if you’re working on a shared branch with other developers because of how Git rewrites commits when rebasing.
