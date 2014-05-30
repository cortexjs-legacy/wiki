# cortex.json

这里将说明 cortex 文件中各个属性的用法及含义。

请注意，cortex.json 文件中的所有定义，需要完全严格遵守 [JSON](http://www.json.org/) 语法，否则 cortex 会有相关报错信息。

```json
{
  "name": "calendar",
  "description": "creates flexiable calendars.",
  "version": "1.0.2",
  "main": "lib/calendar.js",
  "dependencies": {
    "jquery": "~1.9.2"
  },
  "devDependencies": {
    "assert": "*"
  },
  "keywords": [
    "ui",
    "calendar"
  ],
  "directories": {
    "css": "css"
  }
}
```

## name

必须为一个包定义一个 `name`

## version

这个属性必须被定义，它用来描述当前包的版本信息。

为了让他人能够更加安全的使用你的组件，请严格遵循 [语义化版本控制](http://semver.org/lang/zh-TW/) 来设定 `version` 的值。

## description

类型 `string`

为了让其他人更好的使用你的组件，你应该简要地描述该组件包的作用。

## keywords

类型 `Array.<string>`

为了让你的组件包能够更加精确地被用户搜索到，你应该设置这个属性。

## <del>remotes</del>, <del>registry</del>

cortex 不允许在 cortex.json 中定义类似的属性，在我们的规范中，我们**严格地区分项目配置与开发环境配置**，不希望任何这方面的混用。如果你需要改变源服务器的地址，可以使用 [`cortex config`](../cortex/commands/cortex-config.md) 命令。


## main

类型：`path`

它定义了当前模块的主入口 JavaScript 文件，该文件的 `exports` 变量会作为 `require()` 方法的返回值。类似于 `package.main`。

## entries

类型：`String | Array.<String>`

`entries` 用来定义项目中的子入口。在开发的过程中，我们希望能够将子模块的粒度尽量拆分，但是项目发布后，我们又不希望粒度过细而引起文件过多。

这个 field 起到一个模块内部预先打包的作用。

#### 特别说明及约定

当没有定义 entries 的时候，cortex 打包的过程，会将从 `main` 入口，将所依赖到的当前包中的 JavaScript 文件打包到一起。

而设计 entries 的目的，是能够让 `main` 文件能够去动态加载（`require.async`）这些模块，并且在使用的时候再去加载这些模块。

但是需要特别指出的是，**禁止调用外部模块的** entry 文件。

#### 用法

`entries` 可以为

- `String` 相对路径（相对项目根目录），如 `'entries/a.js'`
- `globstar` linux 中的 **globstar** 描述。比如 `'entries/**/*.js'` 指代 entries 目录下所有的 JavaScript 文件，并且同时包含 entries 的子目录；
- `Array` 包含上面某一种或两种类型字符串的数组。

比如 

```json
{
  "entries": [
    "entries/*.js", 
    "pages/a.js"
  ]
} 
```
		
指代 entries 目录下所有的 JavaScript 文件（但不包含子目录），以及 "pages/a.js" 这个 JavaScript 文件。


## ignores

类型： `Array.<Path>`，默认值为：

```js
[
  '.git',
  '.svn',
  '.DS_Store'
]
```

它会告诉 cortex，在发布到 cortexjs.org（或者你自己搭建的服务器）的时候，需要忽略哪些文件。

默认情况下，cortex 会尝试去读取项目跟目录下的 .cortexignore，若该文件不存在，则会依次尝试读取 .npmignore, .gitignore, 但需要注意的是，cortex 仅读取顺序第一个存在的配置文件。

这些文件需要使用 [.gitignore 的规范](http://git-scm.com/docs/gitignore) 来编写（中国本土的用户可能需要翻墙）。


## directories

遵照 [CommonJS Packages](http://wiki.commonjs.org/wiki/Packages/1.0) 规范，我们可以使用 `cortex.directories` 来说明某一个项目的目录结构。

在 Web 开发中，每个目录代表的意义会与 node.js 的开发不同，因此我们创建了一个 `cortex.directories` 的属性来做有些类似的事情。

### directories.dist

无默认值

若 `directories.dist` 已经定义，那么 cortex build 认为 `directories.dist` 中的文件已经预编译完成，而不会进行额外的处理。

但需要注意的是，如果 `scripts.prebuild`（下面会讲到）已经定义，那么在执行 cortex build 命令的时候，仍然会执行 `scripts.prebuild` 的脚本 ———— 但会跳过 cortex 预设的预编译脚本。

如果你想要跳过 cortex 自建的 “编译器” 这是最推荐的方式。

**当然，大多数的情况下，如果你不了解接下来会发生什么，非常建议不要这样做。**

### <del>directories.lib</del>

目前这个值没有直接使用，而更多地根据 `cortex.main` 属性来确定入口 JavaScript 文件的位置。

### directories.css

无默认值

它用来说明 CSS 文件所存放的目录。如果这个值被定义了，但是 `directories.css` 对应的目录不存在，则会报错。

#### 特殊说明

如果你的项目中使用了 less（sass，或 stylus 等），则不能够将这些文件放到 `directories.css` 所指定的目录，这个目录中应该存放编译后的文件。

这种情况下，可以将 less 等脚本编译到 `directories.css` 做指定的目录，并且可以使用 `scripts.prebuild` 来指定编译 less 需要的脚本命令，比如：

```json
{
  "scripts": {
    "prebuild": [
      "grunt less"
    ]
  },
  "directories": {
    "css": "built_css"
  }
}
```

并且将 less 脚本编译到 `'built_css'` 目录。

### directories.template

用来存放模板文件。

无默认值。如果这个值被定义了，但是 `directories.template` 对应的目录不存在，则会报错。


如果 `directories.template` 已经定义，那么会尝试将这个值所对应的目录进行发布。

在将来的版本中，`directories.template` 将会有特殊的作用，因此避免将非模板的文件放到该目录中。

#### 版本要求

Cortex 3.27.0 及以上，neuron 5.1.0 及以上。


### directories.src

用来存放除 JavaScript，CSS，及模板文件之外的资源文件。该目录下的文件，可以通过 `require.resolve(path)` 来获取（要求 [neuron](https://github.com/kaelzhang/neuron) 版本至少为 5.1.0）。

无默认值，如果这个值被定义了，但是 `directories.src` 对应的目录不存在，则会报错。

假若项目结构为：

```text
root/
   |-- source/
            |-- avatar.png
   |-- index.js
```

cortex.json:

```json
{
  "directories": {
    "src": "source"
  }
}
```

index.js 中的代码片段：

```js
// Cortex 的一个设计原则就是，不能违背开发者的直觉。
// 在开发的过程中，我们只需要去关心相对于当前的 JavaScript 文件，相对路径是如何来写就 ok。
var default_avatar = require.resolve('./source/avatar.png');
// -> `default_avatar` 会得到一个绝对路径。
```

#### 特别说明

我们要永远避免在代码中出现任何有关静态文件服务器相关的代码，比如 domain，静态文件根目录，否则在未来，你的代码就是不可维护的。

我们需要能够根据实际情况——比如 CDN 服务出现故障，某个城市用户无法访问静态文件——能够快速地切换所有的静态文件的域名，甚至是 CDN 运营商，这就要求我们的代码中不会出现 **硬代码** 。

`directories` 的设计，目的是要让每个模块本身是内聚的。

#### 版本要求

Cortex 3.27.0 及以上。

## dependencies

类型为 `Object`

与 node.js 开发的 `dependencies` 类似, `cortex.dependencies` 用来定义当前模块的依赖项及版本。

#### 特别说明

绝大多数情况下，你 **不需要也非常不建议** 手工修改这个属性，你可以使用 `cortex install` 的 `--save` 参数，使用该参数后，不仅会将指定的模块安装到本地电脑，同时也会将模块名字和版本信息存储到当前 cortex.json 的 `dependencies` 中。

```sh
cortex install jquery --save
```

## asyncDependencies

类型为 `Object`

用来定义当前模块的动态依赖。

类似的，你可以使用 `cortex install xxx --save-async`，来写入这个值。


## scripts

用于用户自定义命令行脚本。它的作用类似于 hooks，能够在不同的生命周期中被执行。

详见 [cortex-scripts.md](./12_cortex-scripts.md)

#### scripts.prebuild

类型为 `String` 或者 `Array.<string>`

该脚本会在 cortex build 命令的准备阶段执行。比如模块自己使用的 grunt 命令等。

如果有多条命令，请注意要写成 **数组** 的形式。目前还不支持 bash 的 pipe（`'|'`），如果需要这么做，可以使用 Makefile 来实现。

```json
{
  "scripts": {
    "build": "grunt"
  }
}
```

也可以包含多条命令：

```json
{
  "scripts": {
    "prebuild": [
      "grunt dev",
      "grunt"
    ]
  }
}
```

## 补充说明 

如果 cortex 检测不到 cortex.json 的存在，则会尝试去获取 package.json 中的 `cortex` 属性。

**但是我们非常不推荐这么做，并且有可能在未来的某个版本不再支持。**

1. 为了避免跟原有的 package.json 的属性冲突，我们加入了一个新的命名空间 `'cortex'`。若未特别说明，下面的属性都是在 `'cortex'` 这个 field 之下。
2. 对于某一个特定的属性，cortex 会优先读取 `'cortex'` field 中的属性，若读取不到，会尝试去读取 package.json 中的属性，如果仍然读取不到，则会认为是没有定义。
