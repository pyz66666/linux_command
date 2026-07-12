# chown

## 将文件所有者改为 nginx
```bash
sudo chown nginx /var/log/app/error.log
ls -l /var/log/app/error.log
```
```
-rw-r--r-- 1 nginx root 45678 Jul 12 10:30 /var/log/app/error.log
```
> 所有者变为 nginx，组保持 root，nginx 进程现在可以写这个日志文件。

## 同时修改所有者和组
```bash
sudo chown nginx:www-data /var/www/html/index.html
ls -l /var/www/html/index.html
```
```
-rw-r--r-- 1 nginx www-data 1234 Jul 12 10:30 /var/www/html/index.html
```
> `OWNER:GROUP` 语法一次改两者，nginx 是所有者、www-data 是所属组。

## 递归修改目录所有者
```bash
sudo chown -R www-data:www-data /var/www/myapp
```
> `-R` 递归修改目录树下所有文件的所有者和组，恢复 Web 目录权限。

## 只修改组
```bash
sudo chown :developers project/ -R
ls -ld project/
```
```
drwxr-xr-x 3 alice developers 4096 Jul 12 10:30 project/
```
> `:developers` 前面留空只改所属组，project/ 下所有文件现在属于 developers 组。

## 从参考文件复制所有者
```bash
sudo chown --reference=/var/www/index.html /var/www/about.html
ls -l /var/www/index.html /var/www/about.html
```
```
-rw-r--r-- 1 www-data www-data 2345 Jul 12 10:30 /var/www/index.html
-rw-r--r-- 1 www-data www-data 1234 Jul 12 10:30 /var/www/about.html
```
> `--reference` 将 about.html 的所有者和组设置为与 index.html 一致。
