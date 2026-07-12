# mkdir

## 创建单个目录
```bash
mkdir project
```
```
```
> 无输出即成功，在当前目录创建 `project` 目录。

## 递归创建多层目录
```bash
mkdir -p /data/app/{logs,config,backup}
```
```
mkdir: created directory '/data/app'
mkdir: created directory '/data/app/logs'
mkdir: created directory '/data/app/config'
mkdir: created directory '/data/app/backup'
```
> `-p` 自动创建不存在的父目录，花括号展开为多个同级子目录。

## 创建目录并设置权限
```bash
mkdir -m 700 ~/private
```
```
```
> `-m 700` 创建后只有所有者可读写执行，其他人无权访问。

## 创建并显示详情
```bash
mkdir -v docs src tests
```
```
mkdir: created directory 'docs'
mkdir: created directory 'src'
mkdir: created directory 'tests'
```
> `-v` 显示每个被创建的目录，一次可创建多个。

## 确保目录存在（幂等）
```bash
mkdir -p /var/cache/myapp
```
```
```
> `-p` 目录已存在时不报错，适合脚本中确保路径存在。
