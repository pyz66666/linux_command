# usermod

## 将用户加入附加组
```bash
sudo usermod -a -G docker alice
groups alice
```
```
alice : alice docker
```
> `-aG` 追加到 docker 组（必须加 `-a`，否则会替换掉原有的所有附加组）。

## 修改用户登录 shell
```bash
sudo usermod -s /usr/bin/zsh alice
grep alice /etc/passwd
```
```
alice:x:1001:1001::/home/alice:/usr/bin/zsh
```
> shell 从 `/bin/bash` 变为 `/usr/bin/zsh`，修改前需确认 zsh 已安装。

## 修改用户主目录并迁移文件
```bash
sudo usermod -d /data/home/alice -m alice
ls -la /data/home/alice
```
```
total 28
drwxr-xr-x 3 alice alice 4096 Jul 12 10:30 .
-rw-r--r-- 1 alice alice  220 Jul 12 10:30 .bashrc
-rw-r--r-- 1 alice alice    0 Jul 12 10:30 data.txt
```
> `-d` 设新主目录路径加 `-m` 将旧目录内容自动迁移过来，文件所有权不变。

## 锁定和解锁用户
```bash
sudo usermod -L alice
sudo usermod -U alice
```
> `-L` 在密码前加 `!` 锁定（禁止密码登录），`-U` 解锁，与 `passwd -l/-u` 等效。

## 修改用户名
```bash
sudo usermod -l charlie alice
grep charlie /etc/passwd
```
```
charlie:x:1001:1001::/home/alice:/bin/bash
```
> `-l` 将用户名从 alice 改为 charlie，UID 和主目录不变（目录名需手动重命名）。

## 设置账户过期日期
```bash
sudo usermod -e 2026-12-31 bob
sudo chage -l bob | grep "Account expires"
```
```
Account expires: 12月 31, 2026
```
> `-e` 设置账户过期日，过期后无法登录，适合临时账户管理。
