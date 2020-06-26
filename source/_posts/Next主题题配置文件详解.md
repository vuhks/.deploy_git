---
title: Next主题题配置文件详解
tags: [blogs,Hexo]
date: 2020-05-29 23:11:02
abbrlink: hexo-next2
categories: blogs
description: [位于`/theme/next/_config.yml`文件是配置next主题的开关]
---
位于`/theme/next/_config.yml`文件是配置next主题的开关    
以下解释每部分代码控制的什么部分  
详细配置含义可参见[Next主题入门](https://theme-next.js.org/docs/getting-started/)
# 主题核心配置
Theme Core Configuration Settings
## override
false：则将`_data / next.yml`中的配置合并到默认配置中  
true: 则会使用`_data / next.yml`中的选项完全覆盖默认配置（覆盖）。 仅适用于NexT设置。如果为true，则必须将默认NexT`_config.yml`中的所有配置复制到`next.yml`中
## reminder
控制台提示是否发布了新版本
## cache
是否允许缓存内容生成
## minfy
`hexo generate`后是否删除不必要的文件，默认是false
## custom_file_path
自定义文件路径，如果启用，在站点目录`source / data`中创建自定义文件，并在下面取消注释所需的文件。  
```
  head: source/_data/head.swig
  header: source/_data/header.swig
  sidebar: source/_data/sidebar.swig
  postMeta: source/_data/post-meta.swig
  postBodyEnd: source/_data/post-body-end.swig
  footer: source/_data/footer.swig
  bodyEnd: source/_data/body-end.swig
  variable: source/_data/variables.styl
  mixin: source/_data/mixins.styl
  style: source/_data/styles.styl
```
# 网站信息设置
## favicon
网站图标
```
  small: /images/favicon-16x16-next.png
  medium: /images/favicon-32x32-next.png
  apple_touch_icon: /images/apple-touch-icon-next.png
  safari_pinned_tab: /images/logo.svg
  android_manifest: /images/manifest.json
  ms_browserconfig: /images/browserconfig.xml

```
## language_switcher
页脚显示多语言开关按钮，默认不启用

## footer 页脚设置
### since: 2015
指定网站设置的日期。 如果未定义，将使用当前年份。
### icon
```shell
name: fa fa-heart #Font Awesome中的图标名称
animatted: false #icon是否支持动画
color:"ff0000" # 使用十六进制改变颜色
```
### coyright
如果定义为flase，则从站点配置文件`_config.yml`中读取`author`
### powered
是否显示powered by Hexo & false
### beian
国内备案用户显示  
creative_commons:备案信息
```shell    
icp:             #The digit in the num of gongan beian.
gongan_id        #The full num of gongan beian.
gongan_num       # The full num of gongan beian.
gongan_icon_url  # The icon for gongan beian. See: http://www.beian.gov.cn/portal/download
```
### creative_commons
Creative Commons 4.0国际许可
```shell
  license: by-nc-sa #其他可用的证书 by | by-nc | by-nc-nd | by-nc-sa | by-nd | by-sa | zero
  sidebar: false
  post:    false
  language:          #如果您喜欢CC许可证的翻译版本，可以设置语言值 https://creativecommons.org
```
# schemes
主题方案选择，从next主题自带的四种里选择一种
```
scheme: Muse
scheme: Mist
scheme: Pisces
scheme: Gemini
```
Muse Mist是单栏，Pisces和Gemin是双栏
### darkmode
暗黑模式，根据浏览器自动切换为暗黑
## 菜单设置

