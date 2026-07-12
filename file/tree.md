# tree

## 查看目录结构（限制深度 2 层）
```bash
tree -L 2 ~/project
```
```
/home/alice/project
├── README.md
├── src
│   ├── main.py
│   ├── utils.py
│   └── config
├── tests
│   ├── test_main.py
│   └── test_utils.py
└── docs
    └── api.md

4 directories, 6 files
```
> 树形展示目录层级，最后一行统计目录和文件总数。

## 只显示目录
```bash
tree -d -L 2
```
```
.
├── src
│   └── config
├── tests
└── docs

3 directories
```
> `-d` 只输出目录，不显示文件，结构更清晰。

## 显示隐藏文件和文件大小
```bash
tree -ah
```
```
.
├── [ 1.2K]  README.md
├── [  120]  .env
├── [ 4.0K]  src
│   ├── [ 850]  main.py
│   └── [ 512]  utils.py
└── [ 4.0K]  tests
    ├── [ 320]  test_main.py
    └── [ 280]  test_utils.py

3 directories, 6 files
```
> `-a` 显示隐藏文件，`-h` 以人类可读大小显示每个文件。

## 排除特定目录
```bash
tree -I "node_modules|.git"
```
```
.
├── README.md
├── package.json
├── src
│   ├── index.js
│   └── utils.js
└── tests
    └── test.js

2 directories, 5 files
```
> `-I` 排除匹配的目录，此处跳过了 `node_modules` 和 `.git`。

## 显示每个文件的完整路径
```bash
tree -f
```
```
.
├── ./README.md
├── ./src
│   ├── ./src/main.py
│   └── ./src/utils.py
└── ./tests
    ├── ./tests/test_main.py
    └── ./tests/test_utils.py
```
> `-f` 每个文件显示从根开始的完整相对路径。
