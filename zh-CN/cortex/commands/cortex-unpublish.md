# cortex-unpublish(1)

从 registry 中移除一个包的某个版本，或者移除整个包。如果包被移除，那么接下来你将失去对该模块的管理权限。

**注意，未来的某个版本，也许我们会不再允许移除包。**

**`cortex unpublish` 是危险的操作，请三思。**

## 概述

```bash
cortex unpublish [options]
cortex unpublish <name>[@<version>] [options]
```

- name `String` 要移除的包名
- version `SemVer` 要移除的包的版本号 

你必须要拥有对该模块的管理权限，否则将无法进行此操作。


### `cortex unpublish`

这种情况下，cortex 会尝试从当前目录中去读取包的信息，并尝试移除整个包。如果当前工作目录（current working directory）不在某一个 cortex 项目中，则会报错。

但是，要移除整个包，必须要使用 `--force` 参数，否则 cortex 会拒绝你的操作。

因此，实际上大部分操作，我们是使用：

```bash
cortex unpublish --force
```

### `cortex unpublish <name> --force`

移除整个名为 `name` 的包。

### `cortex unpublish <name>@<version>`

移除某个包的特定版本。

### 其他参数

- `--cwd <cwd>` 改变当前命令的工作目录，当你在进行 CI 设置的时候，这个参数会比较有用。 