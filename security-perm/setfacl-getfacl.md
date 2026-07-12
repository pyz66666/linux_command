# setfacl / getfacl

## 查看文件 ACL
```bash
getfacl project/
```
```
# file: project/
# owner: alice
# group: developers
user::rwx
user:bob:r-x
group::rwx
group:auditors:r--
mask::rwx
other::---
default:user::rwx
default:group::rwx
default:mask::rwx
default:other::---
```
> bob 有 r-x 权限（不属于 developers 组），auditors 组有只读权限，`default:` 条目表示子文件会继承。

## 给特定用户添加权限
```bash
setfacl -m u:bob:rw- report.txt
getfacl report.txt
```
```
# file: report.txt
# owner: alice
# group: developers
user::rw-
user:bob:rw-
group::r--
mask::rw-
other::r--
```
> `-m u:bob:rw-` 给 bob 添加读写权限，`ls -l` 会显示 `-rw-rw-r--+` 末尾 `+` 表示有 ACL。

## 设置默认 ACL 让子文件继承
```bash
setfacl -m d:g:developers:rwx shared/
touch shared/newfile.txt
getfacl shared/newfile.txt
```
```
# file: shared/newfile.txt
# owner: alice
# group: alice
user::rw-
group::r--
group:developers:rwx       #effective:rw-
mask::rw-
other::---
```
> 新建文件自动继承 developers 组的 ACL，`#effective:rw-` 表示 mask 限制了实际权限为 rw-。

## 删除特定 ACL 条目
```bash
setfacl -x u:bob report.txt
getfacl report.txt | grep bob
```
> `-x` 删除 bob 的 ACL 条目，确认不再有 bob 相关的权限行。

## 递归备份和恢复 ACL
```bash
getfacl -R project/ > acl_backup.txt
setfacl --restore=acl_backup.txt
```
> `-R` 递归导出整个目录树的 ACL 到文件，`--restore` 恢复，用于迁移或灾难恢复。

## 删除所有扩展 ACL
```bash
setfacl -b report.txt
ls -l report.txt
```
```
-rw-r--r-- 1 alice developers 1234 Jul 12 10:30 report.txt
```
> `-b` 清除所有 ACL 只保留传统 rwx 权限，`ls -l` 末尾的 `+` 消失。
