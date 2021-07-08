# 杭电指北，做不一样的指南

## 项目背景

杭电指北知识库逐渐完善，但是语雀的公开知识库无法让搜索引擎收录到，会缺少来自搜索引擎的流量。

## 项目目的

基于[语雀开放的API](https://www.yuque.com/yuque/developer)实现一套前端的页面，用于提供更好的阅读体验，类似于：[https://sustech.online](https://sustech.online)；
同时接入我们的域名：hduer.cn，移除语雀“登录”的广告，提供更好的用户体验。

## 项目方案

### v0.1 (人工操作：人工智能)

基于语雀的文档导出，将所有文档导出为markdown，然后同步到hexo上面，实现文档的更新。

### v1.0 markdown生成静态网页

使用hexo或者vuepress都是将文章写成markdown的形式，放入指定的目录，然后hexo或者vuepress根据你的markdown文件渲染生成HTML静态文件，从而实现站点的生成与更新（将HTML文件推送到Github即可完成更新）。

- 具体措施

编写脚本，基于脚本通过语雀的API获取文章的markdown数据，将数据写入指定的目录下面，完成后调用hexo等进行markdown的渲染，然后更新网页。

- 缺点，丢失语雀的许多样式，更新成本高（需要调用许多次语雀API，且API有次数限制，不能频繁更新，无法单独针对某篇文章进行更新，一次只能更新全部文档）
- 优点，有人编写了插件，实现成本低，上手快。

### v2.0 基于API实现单页应用

类似于 blog.dreamer2q.wang 这个方案，通过前端调用API获取语雀的数据，然后渲染HTML页面，实现文章的显示。

- 具体措施

提供一台代理服务器，配置好语雀的Token以供前端调用。

- 缺点，成本高，需要有人来编写单页应用，同时需要提供服务器等资源。最重要的无SEO，搜索引擎无法收录（指某度）。
- 优点，文章和语雀完全保持同步，无需构建的过程。

### v3.0 SSR

v2.0没用解决SEO的问题，这次可以交给服务端渲染完成。由于服务端只需要渲染一次即可（因为文章都是静态的），因此可以进行缓存（同步到Github上面），同时服务端渲染的过程也可以交给Github action来完成，进而实现零成本建站。

- 具体措施

完成v2.0，迁移单页应用到SSR上面，并进行缓存（保存渲染后的静态页面）。之后通过脚本将这些页面上传到github完成网站的更新过程，需要使用到语雀的webhook和Github的webhook。

- 缺点，对人的要求比较高。
- 优点，零服务器成本，自带SEO。

### v4.0 自建lake染引擎

基于v3.0更换HTML源为lake格式，完美呈现语雀的原始样式，同时扩展语雀的样式，实现一次大更新。

- 具体措施，无

## 参考链接

- [https://github.com/ulivz/vuepress-plugin-yuque](https://github.com/ulivz/vuepress-plugin-yuque)
- [https://www.yuque.com/u46795/blog/dlloc7](https://www.yuque.com/u46795/blog/dlloc7)



