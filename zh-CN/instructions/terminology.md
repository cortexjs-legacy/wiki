# 术语表

为了帮助开发者精确的理解 cortex 相关文档的说明，这里罗列关键的术语的精确定义。

## registry/包仓库

用于存放 packages 的仓库，类似于 maven 伺服器，gem 源等。


## package/包

1. package 用于描述一个包含 package.json 或者 cortex.json 的项目。
2. 一个 package 中，可能会包含多个 module（模块）
3. 一个 package 只会包含一个入口模块，我们称之为 main（主入口）


## module/模块

1. module 是一个完成独立的功能的单元
2. 一个 package 可能有一个，或者多个 module 来组成
3. 在文件结构上，一个 module 对应一个包含 `exports` 的 JavaScript 文件。


## facade/门面

