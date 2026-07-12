# umask

## 查看当前 umask
```bash
umask
umask -S
```
```
0022
u=rwx,g=rx,o=rx
```
> 当前 umask=022，新建文件=644(rw-r--r--)，新建目录=755(rwxr-xr-x)。

## 验证默认权限
```bash
touch test.txt
mkdir testdir
ls -l
```
```
-rw-r--r-- 1 user user    0 Jul 12 10:30 test.txt
drwxr-xr-x 2 user user 4096 Jul 12 10:30 testdir
```
> 文件 644=666-022，目录 755=777-022，确认 umask 生效。

## 临时设置严格权限
```bash
umask 077
touch secret.txt
ls -l secret.txt
```
```
-rw------- 1 user user 0 Jul 12 10:30 secret.txt
```
> umask 077 后新建文件=600（仅所有者可读写），当前 shell 会话有效。

## 设置组成员可写
```bash
umask 002
touch shared.txt
ls -l shared.txt
```
```
-rw-rw-r-- 1 user user 0 Jul 12 10:30 shared.txt
```
> umask 002 后新建文件=664（组成员也可写），适合团队共享目录。

## 安全级别最高
```bash
umask 027
mkdir private
ls -ld private
```
```
drwxr-x--- 2 user user 4096 Jul 12 10:30 private
```
> umask 027 后新建目录=750，组可读+执行，其他人无任何权限。
