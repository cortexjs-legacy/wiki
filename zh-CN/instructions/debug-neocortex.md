# 在线调试 neocortex 项目

Neocortex 是一个与 cortex 配合的后端工具集，前后端互相融合，能够让调试变得便捷。

如果你的项目，后端使用了 neocortex 进行静态文件的管理，则可以使用下面的方式来进行方便的在线调试。

## 调试用的 Cookie

### cortex_compress

类型 `Boolean=true`，默认为 `true`

用来指定，页面中是否应该输出 **压缩的** CSS 和 JavaScript 文件。这个 cookie 同时会影响到 combo 文件是否会压缩

### cortex_combo

类型 `Boolean=true`，默认为 `true`

用来指定，页面中的 CSS 或者 JavaScript 文件是否要合并到一起变成一个文件来输出。

可以在浏览器的 console 中运行以下代码关闭 combo

```
// 为了避免混乱，设置 path 为 `/`
document.cookie = 'cortex_combo=false; path=/'
```

### cortex_path

类型 `String`，无默认值

用来指定静态文件的服务器地址，为了安全性考虑，仅允许 `http(s)://localhost:<port>` 的地址。 



## chrome 插件 cortex-cookie-manager

[cortex-cookie-manager](https://chrome.google.com/webstore/detail/cortex-cookie-manager/gdcahccbgbmjkadajipnfjloflibhjop?hl=en-US) 是专门配合 neocortex（服务器端中间件）来使用的浏览器插件（目前仅提供 chrome 插件）。

如果网站的后端使用了 neocortex，开发者浏览器中安装了该插件后，点击浏览器工具栏中的 ![chrome-icon](https://raw.github.com/cortexjs/cortex/master/screenshots/chrome-icon.png) 图标，页面中的静态文件（目前仅支持 JavaScript）都会指向本地的 cortex server。

接下来 cortex server 会启动好全套的本地服务以供调试。