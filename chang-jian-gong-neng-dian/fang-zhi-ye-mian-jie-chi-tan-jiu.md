# 防止页面劫持探究

# 背景

产品发来一张截图, 是我们的支付页面里被嵌入了一个竞品的广告

产品大发雷霆, 说无论如何也要尽快把这些广告干掉

然而最稳的方法就是切https啊...但是这在已经发展了几年的域名网站里...

这可是一项大工程哇.....

所以只能另辟蹊径...

# Content Security Policy

这个是现代浏览器中最稳的方式了

语法: 一个指令的多个值用英文空格分开, 多个指令间用

## 指令

| 指令        | 说明                                                                                                                                        |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| default-src | 定义针对所有类型（js、image、css、web font，ajax 请求，iframe，多媒体等）资源的默认加载策略，某类型资源如果没有单独定义策略，就使用默认的。 |
| script-src  | 定义针对 JavaScript 的加载策略。                                                                                                            |
| style-src   | 定义针对样式的加载策略。                                                                                                                    |
| img-src     | 定义针对图片的加载策略。                                                                                                                    |
| connect-src | 针对 Ajax、WebSocket 等请求的加载策略。不允许的情况下，浏览器会模拟一个状态为 400 的响应。                                                  |
| font-src    | 针对 WebFont 的加载策略。                                                                                                                   |
| object-src  | 针对 、 或,等标签引入的 flash 等插件的加载策略。                                                                                            |
| media-src   | 针对,或,等标签引入的 HTML 多媒体的加载策略。                                                                                                |
| frame-src   | 针对 frame 的加载策略。                                                                                                                     |
| sandbox     | 对请求的资源启用 sandbox(类似于 iframe 的 sandbox 属性)[https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe]）。                                                                                 |
| report-uri  | 告诉浏览器如果请求的资源不被策略允许时，往哪个地址提交日志信息，只提交日志，不阻止任何内容(仅对Content-Security-Policy-Report-Only头有效)。 |

# 参考链接

1. CSP2的w3文档 https://www.w3.org/TR/CSP2/
