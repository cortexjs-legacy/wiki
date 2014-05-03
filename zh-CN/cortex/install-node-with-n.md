# 使用 n 来安装和管理 node

n 类似于 Ruby 的 [RVM](https://rvm.io)，可以方便的安装特定版本的 node 和管理 node 的版本。

好，不废话了：

## Github

[https://github.com/visionmedia/n](https://github.com/visionmedia/n)

## 安装 n

大部分情况，只需要 `git clone` 然后 `make install` 即可：

```bash
git clone git@github.com:visionmedia/n.git
cd n
make install # 可能需要 sudo
```

如果已经安装过 node，你可以使用 npm 来安装 n

```bash
npm install -g n
```

## 使用

#### 安装并使用最新版本的 node

```bash
n latest
```

#### 安装并使用特定版本（甚至是非正式发布的非稳定版本）

```bash
n 0.11.13 # 写这个文档的日期是 2014-05-03
```

其他使用方法不累述，请查看文档，或者运行 `n -h`