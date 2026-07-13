# docker build

## 从当前目录 Dockerfile 构建
```bash
docker build -t myapp:v1 .
```
```
[1/5] FROM node:18-alpine
[2/5] WORKDIR /app
[3/5] COPY package*.json ./
[4/5] RUN npm ci --only=production
[5/5] COPY . .
Successfully built a1b2c3d4e5f6
Successfully tagged myapp:v1
```
> `-t` 命名并打标签，`.` 指定构建上下文为当前目录，输出显示每一步的进度。

## 指定 Dockerfile 路径
```bash
docker build -t myapp:v2 -f docker/Dockerfile.prod .
```
```
Successfully built f6e5d4c3b2a1
Successfully tagged myapp:v2
```
> `-f` 指定 Dockerfile 路径，构建上下文仍然是 `.`，可以用不同的 Dockerfile 生成不同环境的镜像。

## 构建时不使用缓存
```bash
docker build --no-cache -t myapp:v1 .
```
```
Step 1/5 : FROM node:18-alpine
 ---> a1b2c3d4e5f6
...
```
> `--no-cache` 强制从头构建所有层，不利用已缓存的中间层，适合排查缓存导致的问题。

## 传入构建参数
```bash
docker build --build-arg APP_ENV=production -t myapp:prod .
```
```
Successfully tagged myapp:prod
```
> `--build-arg` 传入构建时变量，Dockerfile 中用 `ARG APP_ENV` 接收。
