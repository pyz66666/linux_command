# useradd / userdel

## 创建标准用户
```bash
sudo useradd -m -s /bin/bash alice
sudo passwd alice
id alice
grep alice /etc/passwd
```
```
uid=1001(alice) gid=1001(alice) groups=1001(alice)
alice:x:1001:1001::/home/alice:/bin/bash
```
> `-m` 创建主目录 `/home/alice`，UID/GID=1001，登录 shell 为 bash。

## 创建属于多个组的用户
```bash
sudo useradd -m -s /bin/bash -G sudo,docker,developers bob
id bob
```
```
uid=1002(bob) gid=1002(bob) groups=1002(bob),27(sudo),999(docker),1000(developers)
```
> `-G` 指定附加组，bob 同时属于 sudo（可执行 root 命令）、docker、developers 组。

## 创建系统用户
```bash
sudo useradd -r -s /usr/sbin/nologin myapp
grep myapp /etc/passwd
```
```
myapp:x:998:998::/home/myapp:/usr/sbin/nologin
```
> `-r` 创建系统用户（UID<1000），`nologin` 禁止登录，用于运行服务进程。

## 指定 UID 创建用户
```bash
sudo useradd -m -u 1500 -s /bin/bash charlie
id charlie
```
```
uid=1500(charlie) gid=1500(charlie) groups=1500(charlie)
```
> `-u` 指定 UID=1500，适合需要与 NFS 或其他系统保持 UID 一致的场景。

## 删除用户及其主目录
```bash
sudo userdel -r alice
grep alice /etc/passwd
```
> 无输出表示已删除，`-r` 同时删除主目录和邮件池，不加 `-r` 则保留主目录。
