﻿前面章节我们介绍了缓存配置，当 CDN 的资源文件缓存过期之后会回源获取文件并缓存，但是这是一个被动更新的过程，资源更新受限于缓存过期时间。当源站资源更新之后需要快速回源下发到 CDN 节点时，可以使用缓存刷新功能来实现，这是一种主动更新的方式。

**配置引导**

登录 [CDN 控制台](https://console.upyun.com/login/)，进入 `刷新` 栏目，您可以选择 `URL 刷新`、`规则刷新`来强制回源更新文件及目录。您也可以在 `操作记录` 选项查询刷新进度及相关状态。

##URL 刷新

当源站有少量文件更新时，可以使用 `URL 刷新` 来主动删除 CDN 节点上的资源文件。新的请求进来时，CDN 节点会回源获取文件并将新的资源文件缓存至 CDN 节点，所以这是一个主动更新的过程。操作界面如下图所示：

<img src="http://upyun-assets.b0.upaiyun.com/docs/cdn/upyun-cdn-url-refresh.png" height="490" width="800" />


注意事项：

1.每行一个URL地址，每个 URL 地址以 http://或https://开头，例如：`http://example.com/image/test.jpg`

2.每次输入不超过 50 个，刷新任务全网生效时间大约 5 到 10 分钟

##规则刷新

当源站有针对资源进行批量更新时，可以通过 `规则刷新` 来刷新节点缓存文件。实际上，规则刷新并没有删除节点资源文件，规则一旦生效之后，缓存在 CDN 节点的文件会被致过期，新的请求会回源校验一次，如果源站文件有更新，则将新的文件响应给最终用户并替换节点上的旧文件。操作界面如下图所示：

<img src="http://upyun-assets.b0.upaiyun.com/docs/cdn/upyun-cdn-rule-refresh.png" height="490" width="800" />


规则示例：

    http://example.com/image/＊
    http://example.com/image/＊.jpg
    http://example.com/image/＊!upyun（ 适用于自定义缩略图版本 ）


注意事项：

1.每行一个路径规则，每个路径规则以 http:// 或 https:// 开头，每次输入不超过 10
   个，例如：`http://example.com/image/＊`
   
2.规则刷新主要用于对使用客户自主源站的 CDN 服务，执行后会在 10 分钟内生效

特别声明：

1.如您使用了又拍云对象存储服务时，如果您通过 `规则刷新` 来刷新缓存的话，基于平台保护，`规则刷新` 生效时间是 1 个小时，请谨慎操作

2.特别地，使用了又拍云对象存储服务时，存储中资源更新（替换或删除）时会自动触发 CDN 节点刷新缓存，会在 5 分钟内生效，所以您无需进行手动刷新操作

##URL 预热

当源站有新增新的资源文件时，可将这些新文件提前缓存至 CDN 节点，最终用户第一次访问这些资源文件时， CDN 节点不需要回源站请求文件资源了。一方面可减少用户突发访问时的回源量，另一方面可以加快资源文件的首次访问速度。操作界面如下图所示：

<img src="http://upyun-assets.b0.upaiyun.com/docs/cdn/upyun-cdn-url-preheat.png" height="490" width="800" />


注意事项：建议不要同时预热太多资源文件，否则会对源站造成回源压力

##操作记录

进行 `URL 刷新` 、 `规则刷新` 、`URL 预热` 操作之后，界面窗口会立马跳至操作记录界面，您可以实时查看当前操作的进度反馈及相关状态。您也可以查看历史操作记录，我们默认保留了 3 天的数据。

----------