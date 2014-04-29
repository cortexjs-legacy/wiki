# cortex-server(1)

启动 cortex server，这个服务有如下功能：

- 提供本地静态文件服务；
- 能够 **自动** 从代码仓库下载本地缺失的静态包；
- 让其他系统能够去通过 http 的方式来运行一个 cortex 子命令。

## 概述

```bash
cortex server [options]
```

## options

### `--open` 

如果加入这个设置，那么 cortex server 在启动的时候，还会同时尝试在浏览器中打开静态服务的根目录

### `--port <port>` 

指定 cortex server 的端口，默认端口为 9074（9ctx）

