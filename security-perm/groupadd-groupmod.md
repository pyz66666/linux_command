# groupadd / groupmod

## 创建项目组
```bash
sudo groupadd developers
sudo groupadd -r docker
grep -E "developers|docker" /etc/group
```
```
docker:x:998:
developers:x:1001:
```
> developers 是普通组（GID≥1000），docker 是系统组（`-r` 创建 GID<1000）。

## 将用户加入组
```bash
sudo usermod -aG developers alice
sudo usermod -aG developers bob
grep developers /etc/group
```
```
developers:x:1001:alice,bob
```
> 用 `usermod -aG` 将用户追加到组，alice 和 bob 都是 developers 组成员。

## 重命名组
```bash
sudo groupmod -n devops developers
grep devops /etc/group
```
```
devops:x:1001:alice,bob
```
> `-n` 重命名组，GID 保持 1001 不变，文件系统中关联是基于 GID 的所以自动同步。

## 查看用户所属所有组
```bash
groups alice
```
```
alice : alice sudo docker devops
```
> alice 属于 alice（主组）和 sudo、docker、devops（附加组）。

## 修改组 ID
```bash
sudo groupmod -g 2000 devops
grep devops /etc/group
```
```
devops:x:2000:alice,bob
```
> `-g` 将 GID 从 1001 改为 2000，已有文件的组归属需手动用 `find -gid 1001 -exec chgrp` 修复。

## 创建组时使用 force 模式
```bash
sudo groupadd -f developers
```
> 组已存在时不报错直接成功退出，适合脚本中幂等创建。
