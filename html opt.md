# 网页渲染机制与优化策略

## 浏览器如何渲染网页?
- 使用 HTML 创建文档对象模型（DOM）
- 使用 CSS 创建 CSS 对象模型（CSSOM）
- 执行脚本（Scripts）
- 合并 DOM 和 CSSOM 形成渲染树（Render Tree）
- 使用渲染树布局（Layout）所有元素
- 渲染（Paint）所有元素

## HTML 加载优化策略

- 样式在顶部，脚本在底部
总体思路是尽可能早的加载样式，尽可能晚的加载脚本。

- 最小化和压缩
js -> uglify min
js/css -> nginx GZip
image -> inline base64

## CSS 加载优化策略

- 减少冗余样式，按需加载样式
- css in jsx

## JavaScript 加载优化策略
- defer
- async (适用google)

## 浏览器限制
- HTTP1 文件限制
我们浏览器的 HTTP1 协议，在同一个域名，同一次，允许下载的文件数有最大限制，范围从 2（老旧的浏览器）到 6（Edge，Chrome）。
如果网站使用了 HTTP2，并且用户的浏览器也兼容，则可以完全避开这个下载限制。

- TCP 往返限制
每一次服务器往返可以传送的最大数据量是 14kb，包括所有 HTML，CSS 和脚本的网络请求。
如果我们的 HTML，或者积累的资源请求超过 14kb时，需要多做一次服务器往返。
