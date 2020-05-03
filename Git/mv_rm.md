# Move & Remove

## Move
* `git mv <old_place> <new_place>` 最标准的移动方式
* 如果不小心用$mv$移动了文件，可以先将旧文件`git rm`再将新文件`git add`, git会自动识别为移动
* `git add -A <dir>` 也能批量解决文件已经被其他方式移动的问题，即使文件同时被修改和移动
* git 认为改变不超过50%的文件都是同一个文件，即使它被移动了位置。
* `git log --stat -M[similarity_index] --follow -- <file>` 追踪所有关于某个file的提交历史，包括移动之前的提交，
默认similarity index是50，可以调整为其他值，比如99

## Remove
* `git rm <file>` 删除working directory的文件, 并同时删除文件的index(不再跟踪该文件)，若该文件已被`rm`删除，也可以继续使用`git rm`来缓存删除操作
* `git rm --cached <file>` 只删除文件的index
* `git add -u <dir>` 如果用其他的文件管理方式删除了多个文件，可以用这个命令来缓存dir下的所有删除操作
