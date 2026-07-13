# docker exec

## 进入容器执行 shell
```bash
docker exec -it web /bin/sh
```
```
/app #
```
> `-it` 分配交互终端，`web` 是容器名，`/bin/sh` 用于基于 Alpine 的轻量镜像。

## 不进入容器直接执行命令
```bash
docker exec web cat /etc/nginx/nginx.conf
```
```
worker_processes 1;
events { worker_connections 1024; }
http {
    server {
        listen 80;
        ...
    }
}
```
> 在容器内执行单条命令并返回输出，适合快速查看配置文件或日志文件。

## 以指定用户执行
```bash
docker exec -u postgres db psql -c "SELECT version();"
```
```
                          version
------------------------------------------------------------
 PostgreSQL 15.4 on x86_64-pc-linux-gnu
```
> `-u` 以容器内 postgres 用户身份执行命令，避免 root 权限风险。

## 设置环境变量执行
```bash
docker exec -e MYSQL_PWD=secret db mysql -u root -e "SHOW DATABASES;"
```
```
Database
information_schema
mydb
mysql
```
> `-e` 临时设置环境变量（仅此次执行有效），避免密码明文出现在历史记录中。
