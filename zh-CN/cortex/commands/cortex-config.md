# cortex-config(1)

用来修改当前的用户的设置。

## 概述

```bash
cortex config set <key> [<value>]
cortex config get <key>
cortex config delete <key>
cortex config delete --delete-all
cortex config list
cortex config edit
```
   
    
## 描述

在配置上，cortex 与 npm 的配置有很大不同，详见 [cortex-profile(1)](./cortex-profile.md)。

`cortex config` 用于管理那些会影响 cortex 其他命令运行的全局配置。

整体来看，`cortex config` 的用法可以总结为：

```bash
cortex config <sub-command> ...
```

### Sub-commands

其中，可选择的 `<sub-command>` 包括：

#### set

##### set \<key> \<value>

根据 key 来设置一个 config 的值，所有可进行设置的 key，请见 [configurations](#configurations)。

比如，我们可以通过

```bash
cortex config set colors false
```

来关闭 cortex 命令行输出的配色，如果你的系统（比如老版本的 Jenkins）不支持颜色，可以进行这个设置。

##### set \<key>

如果没有传递值，比如 `cortex config set colors`，则 cortex 会进入交互模式来继续设置新的值。

#### get \<key>

获取当前某个 key 的值。

```bash
cortex config get colors
```

#### delete

##### delete \<key>

移除某个值的用户设置，将其还原为默认值。

##### delete --delete-all

全部还原为默认设置。

#### list

列出所有能够被设置的 key

#### edit

在编辑器中打开配置文件。打开什么编辑器，跟当前用户系统的设置有关。
