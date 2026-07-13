# docker cp

## 从主机拷贝文件到容器
```bash
docker cp ./config.yaml web:/etc/nginx/config.yaml
```
> 无输出即成功，将主机当前目录的 `config.yaml` 拷贝到容器 `web` 的 `/etc/nginx/` 下。

## 从容器拷贝文件到主机
```bash
docker cp web:/var/log/nginx/access.log ./access.log
```
```
Successfully copied 2.56kB to ./access.log
```
> 将容器内的日志文件拷贝到主机当前目录，调试时特别有用。

## 拷贝整个目录
```bash
docker cp ./dist web:/usr/share/nginx/html/
```
> 将主机 `dist/` 目录内容拷贝到容器 nginx 的静态文件目录，容器内若已有同名文件会被覆盖。
