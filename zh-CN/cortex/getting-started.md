# 新手指引

## 安装 Cortex

首先，你需要安装 [`node.js`](http://nodejs.org)，并且版本至少需要 0.10.0。推荐大家 [使用 n 来方便的安装 node 和管理 node 版本](./install-node-with-n.md)。

当你安装好 node.js 后，在命令行工具中（比如 mac 的 terminal 或者 iterm）运行以下命令：

```bash
npm install -g cortex
```

根据实际情况，你可能需要使用 `sudo`。

## Hello World！

说明如何来创建一个 hello world 项目，先来看看我们要完成什么：

> 我们希望在页面上，用 JavaScript 输出一段文本：“Hello world!”

#### 使用 cortex init 命令根据脚手架创建新项目

Cortex 标准化每一个新创建的 web 前端项目

```bash
mkdir hello-world
cd hello-world # 创建新项目目录并进入

cortex init # 中间可能会出现安装其他工具的提示，请按照说明进行
```

运行命令后，会出现类似的提示：

```bash
Please answer the following:
[?] Project name (hello-world)
```

根据实际项目的情况，填写需要的内容，这里我们说明一下几个关键提问：

- **Project name**: 是你的项目的唯一名称，类似于 artifactid。你不用担心后续重名的问题，因为 cortex 模块在发布之时，会校验重名的问题。
- **Version**: 项目的版本，我们遵循 [语义化版本](http://semver.org/lang/zh-TW/) 规则。

其他的提问，事实上所有的设置，都可以使用默认，即一路回车到底，因为我们后来还在 package.json 文件中来修改它们。


#### 安装依赖：例如 jQuery

我们想要用 jQuery，在 `<body>` 中插入文字。我们先安装 jQuery

```bash
cortex install jquery --save # 注意，别忘记这里的 --save
```

`--save` 可以将依赖声明加入到 package.json 中，这样其他的开发者使用你的项目的时候，也能够获取到 jquery。大部分的时候，我们都不应该手动去改 package.json 中的依赖。


#### 正式开始开发

用编辑器打开项目中的 index.js，并编辑它，事实上，我们跟 node.js 完全相同的方式来写 web 代码。

```js
var $ = require('jquery');
exports.init = function(){
	$('body').html('Hello world!');
};
```

用编辑器打开 index.html，我们会看到：

```html
<script>
facade({
  mod: 'hello-world'
});
</script>
```

我们来说明一下这一段脚本。`facade(modObject)` 是一个全局的方法，它所做的事请很简单，加载 `modObject.mod` 这个包，并且运行这个包的 `init` 方法，即上面代码中定义的 `exports.init`

#### 运行 cortex build

Cortex build 会进行一些必要的构建工作，也会去调用用户自定义的构建命令，构建会让 node.js 风格的代码能够在浏览器端正常运行。

同时，你能够通过 `cortex watch` 命令来监听文件的变化，当文件内容发生变化的时候，会自动执行 `cortex build` 命令。

#### 浏览结果

在默认的模式下，你需要使用 cortex server 启动本地的静态服务器，在命令行中输入：

```bash
cortex server
```

然后使用浏览器打开 index.html，就会看到页面上输出了 "Hello world!"


## 示例项目

你可以访问 [cortexjs/samples](https://github.com/cortexjs/samples) 项目，来查看上面的 hello world 项目，以及更多的其他示例项目。

这些项目中，会包含详细的注释，以及操作说明。

