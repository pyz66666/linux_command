# chmod

## 给脚本添加执行权限
```bash
chmod +x deploy.sh
ls -l deploy.sh
```
```
-rwxr-xr-x 1 user user 1234 Jul 12 10:30 deploy.sh
```
> `+x` 给所有用户添加执行权限，对应八进制 755（rwxr-xr-x）。

## 设置 Web 目录为 755
```bash
chmod -R 755 /var/www/html
ls -ld /var/www/html
```
```
drwxr-xr-x 5 root root 4096 Jul 12 10:30 /var/www/html
```
> `-R` 递归设置，755=所有者可读写执行，组和其他人只读+执行，目录的 x 权限表示可进入。

## 保护私钥文件
```bash
chmod 600 ~/.ssh/id_rsa
ls -l ~/.ssh/id_rsa
```
```
-rw------- 1 user user 2602 Jul 12 10:30 /home/user/.ssh/id_rsa
```
> 600=仅所有者可读写，SSH 私钥必须设为此权限，否则 ssh 会拒绝使用。

## 保护配置文件仅所有者可读
```bash
chmod 400 /etc/app/secrets.conf
ls -l /etc/app/secrets.conf
```
```
-r-------- 1 root root 128 Jul 12 10:30 /etc/app/secrets.conf
```
> 400=仅所有者可读，适合数据库密码等敏感配置文件。

## 用符号模式精细调整权限
```bash
chmod u+x,g-w,o-r report.txt
ls -l report.txt
```
```
-rwxr----- 1 user user 5678 Jul 12 10:30 report.txt
```
> 符号模式：u+x 所有者加执行、g-w 组去写、o-r 其他人去读，比八进制更直观。

## 从参考文件复制权限
```bash
chmod --reference=template.sh new_script.sh
ls -l template.sh new_script.sh
```
```
-rwxr-xr-x 1 user user 100 Jul 12 10:30 template.sh
-rwxr-xr-x 1 user user 200 Jul 12 10:30 new_script.sh
```
> `--reference` 将 new_script.sh 的权限设置为与 template.sh 完全一致。
