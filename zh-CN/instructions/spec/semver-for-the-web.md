# 为Web扩展的SemVer

## 描述




## 我们为什么需要语义化的版本控制

[Semantic Versioning 的文档](https://github.com/mojombo/semver/blob/master/semver.md#why-use-semantic-versioning) 中，已经解释了这个问题。

## 为什么我们要扩展它？

这个也是 [node.js](http://nodejs.org) 遇到的问题，因此 node.js 的包管理工具 [npm](http://npmjs.org/) 也扩展了 [version range](https://npmjs.org/doc/misc/semver.html)。

#### 然而，对于 web 模块为何我们也需要扩展 semver ？

假若我们遵循 [commonjs](http://wiki.commonjs.org) 的方式来构建 web 模块，并且模块 `foo@1.0.1` 有如下片段：

```js
var $ = require('jquery');
module.exports = function(){
    // ...
};
```

则该模块会包装成类似如下的代码：

```
define(name, ['jquery@1.9.3'], function(require, exports, module){
	var $ = require('jquery');
	module.exports = function(){
	    // ...
	};
});
```

同时，该模块可能会发布到类似 `xxxx/foo/1.0.1/foo.js` 的地址；而 `jquery@1.9.3` 会发布到 `xxx/jquery/1.9.3/jquery.js`。


假若某一天 `jquery` 更新到 `1.9.4`（它是一个 bug fix），我们就需要将

