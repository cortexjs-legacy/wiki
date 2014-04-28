# cortex-install(1)

安装指定依赖或根据 `cortex.json`/`package.json` 中的依赖关系安装相关的模块

## 概述

``` bash
    cortex install 
    cortex install <name>[@<version>] [<module2> <module3>]
    cortex install <name> [--save|--save-dev|--save-async] [--cwd <path>] [--clone]
    cortex install [--production|--no-production] [--recursive|--no-recursive]
```

## 描述

类似`npm install`，安装项目所需要的依赖。可以指定项目名称和版本，如果没有指定项目，则从当前目录 (可以由`--cwd`参数改变) 中的 `cortex.json`|`package.json`中读取当前项目依赖。

```
cortex install // 安装在当前目录中的 `cortex.json`|`package.json` 文件中指定的依赖
```

如果只指定了项目名称而没有指定版本，默认安装 `latest` 版本。

```
cortex install jquery // 等同于 cortex install jquery@latest
```

可以同时指定安装多个项目

```
cortex install request class@1.0.0 lang
```    
## 选项

### `--save|--save-dev|--save-async`

* `--save` 参数会将安装的模块写入到 `package.json` 的 `dependencies` 中。
* `--save-dev` 则只会将依赖安装的模块写到 `package.json` 的 `devDependencies`中，`devDependencies` 中的模块在 使用了 `--production` 参数时会被忽略而不会被安装。
* `--save-async` 则安装的模块会被写入到 `pacakge.json` 的 `asyncDependencies` 中，`asyncDepdnencies` 中的模块会在运行时由loader异步加载。

### `--cwd <path>`

指定命令运行时的目录，覆盖shell中的当前目录。

### `--clone``

在安装模块时，会尝试从模块指明的 repository 中将模块的Repo克隆到当前的工作目录中。

### `--production|--no-production`

设置是否是生产环境，如果是则在安装时忽略 `devDepdnencies` 中的模块, 默认不是生产环境。

### `--recursive|--no-recursive`

是否递归的安装依赖，默认为true；如果为false，这只会安装指定的模块，而不会安装这些模块的依赖模块。
