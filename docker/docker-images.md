# docker images

## 查看本地镜像列表
```bash
docker images
```
```
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
myapp        v1        a1b2c3d4e5f6   2 hours ago    250MB
nginx        alpine    d3f7a8b9c1e2   2 days ago     41MB
mysql        8         a9b8c7d6e5f4   3 weeks ago    519MB
```
> TAG 默认显示，`<none>` 标签通常是无用镜像（构建失败或重复标签产生）。

## 只显示镜像 ID
```bash
docker images -q
```
```
a1b2c3d4e5f6
d3f7a8b9c1e2
a9b8c7d6e5f4
```
> `-q` 只输出镜像 ID，配合 `docker rmi $(docker images -q)` 批量删除。

## 查看悬空镜像
```bash
docker images -f "dangling=true"
```
```
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
<none>       <none>    e5f6a7b8c9d0   1 hour ago     300MB
```
> `-f` 过滤条件，`dangling=true` 显示无标签的中间层镜像，通常可以安全删除。

## 按仓库名过滤
```bash
docker images nginx
```
```
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        alpine    d3f7a8b9c1e2   2 days ago     41MB
nginx        latest    e5f6a7b8c9d0   5 days ago     187MB
```
> 只显示 nginx 仓库下的所有标签镜像。
