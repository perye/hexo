# hexo
[hexo](https://github.com/hexojs/hexo):A fast, simple &amp; powerful blog framework, powered by Node.js.


# Quick Start
## Install Hexo
>$ npm install hexo -g

or

>$ yarn global add hexo

## Setup your blog
>$ hexo init blog

>$ cd blog
## Start the server
>$ hexo server
## Create a new post
>$ hexo new "Hello Hexo"
## Generate static files
$ hexo generate

# 说明
风格采用[hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery)

- 简单漂亮，文章内容美观易读
- Material Design 设计
- 响应式设计，博客在桌面端、平板、手机等设备上均能很好的展现
- 首页轮播文章及每天动态切换 Banner 图片
- 瀑布流式的博客文章列表（文章无特色图片时会有 24 张漂亮的图片代替）
- 时间轴式的归档页
- 词云的标签页和雷达图的分类页
- 丰富的关于我页面（包括关于我、文章统计图、我的项目、我的技能、相册等）
- 可自定义的数据的友情链接页面
- 支持文章置顶和文章打赏
- 支持 MathJax
- TOC 目录
- 可设置复制文章内容时追加版权信息
- 可设置阅读文章时做密码验证
- Gitalk、Gitment、Valine 和 Disqus 评论模块（推荐使用 Gitalk）
- 集成了不蒜子统计、谷歌分析（Google Analytics）和文章字数统计等功能
- 支持在首页的音乐播放和视频播放功能
- 支持emoji表情，用markdown emoji语法书写直接生成对应的能跳跃的表情。
- 支持 DaoVoice、Tidio 在线聊天功能。

## [配置使用](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md#%E9%85%8D%E7%BD%AE)

# 启动
>$ hexo clean

>$ hexo generate

>$ hexo server


# 部署
>$ hexo clean

>$ hexo generate

>$ hexo deploy

注意deploy的过程中要输入你github的username及passward
