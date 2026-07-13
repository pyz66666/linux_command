# docker pull / push

## 拉取镜像
```bash
docker pull nginx:alpine
```
```
alpine: Pulling from library/nginx
Digest: sha256:abc123...
Status: Downloaded newer image for nginx:alpine
```
> 从 Docker Hub（默认）拉取 `library/nginx` 仓库的 `alpine` 标签镜像。

## 从私有仓库拉取
```bash
docker pull registry.example.com/myapp:v1
```
```
v1: Pulling from myapp
Digest: sha256:def456...
Status: Downloaded newer image for registry.example.com/myapp:v1
```
> 指定完整仓库地址拉取，需先 `docker login registry.example.com`。

## 推送镜像到仓库
```bash
docker push registry.example.com/myapp:v1
```
```
The push refers to repository [registry.example.com/myapp]
a1b2c3d4: Pushed
e5f6a7b8: Pushed
v1: digest: sha256:def456... size: 528
```
> 推送时会逐层上传，已存在的层会跳过（Layer already exists）。

## 重新打标签后推送
```bash
docker tag myapp:v1 registry.example.com/myapp:v1
docker push registry.example.com/myapp:v1
```
```
v1: digest: sha256:def456... size: 528
```
> `docker tag` 给镜像加上仓库前缀，再 `push` 到指定仓库，同一个镜像多个标签不占额外空间。
