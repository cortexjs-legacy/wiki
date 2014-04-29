# cortex-publish(1)

将模块发布到 `cortex registry` 上，名称和版本信息都从 `package.json` 文件中读取。

## 概述

``` bash
cortex publish
cortex publish [--cwd <path>]
```

## 描述

发布当前模块，当registry中的模块已经存在的时候，发布将失败，需要使用 `--force` 参数覆盖原有版本。

也可以发布指定的tar包，tar包中必须包含 `package.json` 文件。

``` bash
cortex publish moduleA.tar
```

## 选项

### `--cwd <path>`

指定命令运行时的目录，覆盖shell中的当前目录。

