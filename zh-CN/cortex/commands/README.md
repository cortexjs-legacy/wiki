# Cortex(1)

命令索引。

## 基本命令

### `cortex -h`
### `cortex --help`

查看 cortex 基本命令帮助

### `cortex <command> -h`

查看 `cortex <command>` 的简明帮助。


### `cortex help <command>`

查看 `cortex <command>` 命令的详细帮助，包含使用方法和详细的参数说明。

比如，可以在命令行中运行：

```bash
cortex help install
```


## cortex 子命令

- [cortex-install(1)](./cortex-install.md)
- [cortex-build(1)](./cortex-build.md)
- [cortex-publish(1)](./cortex-publish.md)
- [cortex-unpublish(1)](./cortex-unpublish.md)
- [cortex-watch(1)](./cortex-watch.md)
- [cortex-update(1)](./cortex-update.md)
- [cortex-server(1)](./cortex-server.md)
- [cortex-config(1)](./cortex-config.md)
- [cortex-profile(1)](./cortex-profile.md)
- [cortex-adduser(1)](./cortex-adduser.md)
- [cortex-owner(1)](./cortex-owner.md)

## cortex 其他命令

目前下面的命令是以插件的形式安装


### 如何安装 cortex 插件？

以 `cortex-test` 为例：

```bash
$ npm install -g cortex-test
```

### 官方插件

- [cortex-search(1)](https://github.com/cortexjs/cortex-search)
- [cortex-shrinkwrap(1)](https://github.com/cortexjs/cortex-shrinkwrap)
- [cortex-test(1)](https://github.com/cortexjs/cortex-test)
