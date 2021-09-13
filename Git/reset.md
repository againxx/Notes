# Reset

## Three trees

Three trees in Git
| Tree              | Role                              |
|-------------------|-----------------------------------|
| HEAD              | Last commit snapshot, next parent |
| Index             | Proposed next commit snapshot     |
| Working Directory | Sandbox                           |

Typical workflow involves these three trees
![workflow](https://gitee.com/againxx/image-storage/raw/master/images/20210913130823.png =750x)

## The role of reset
![Initial state](https://gitee.com/againxx/image-storage/raw/master/images/20210913131720.png =750x)

---

**Step 1**: Move HEAD with the branch that HEAD is pointing to (`--soft` will stop here)
![git reset --soft HEAD~](https://gitee.com/againxx/image-storage/raw/master/images/20210913132037.png =750x)

---

**Step 2**: Updating the Index (`--mixed` will stop here)
![git reset --mixed HEAD~](https://gitee.com/againxx/image-storage/raw/master/images/20210913132242.png =750x)

---

**Step 3**: Updating the Working Directory (`--hard` will stop here)
![git reset --hard HEAD~](https://gitee.com/againxx/image-storage/raw/master/images/20210913132426.png =750x)
