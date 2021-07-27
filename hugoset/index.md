# Window环境搭建hugo个人博客


#  Window环境搭建hugo个人博客

---

- 电脑安装并配置Git，尤其是username和email
- 注册GitHub账号，在GitHub配置ssh验证
- 配置环境变量

## 1.github下载Hugo

```
https://github.com/gohugoio/hugo/releases
```

### 配置hugo环境变量,将hugo.exe 配置到系统变量

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/1.png " ") 

### 创建站点

```c#
hugo new site Myblog1
```

## 2.下载主题

```c#
 cd themes
 git clone https://github.com/vaga/hugo-theme-LoveIt.git themes/LoveIt
```

根据主题文档进行简单配置（exampleSite）示例站点



## 3.新增文章本地测试

```c#
hugo new posts/FileName.md
hugo server -t LoveIt --buildDrafts --disableFastRender
```

访问http://localhost:1313/测试是否可访问

## 4.github新建仓库

仓库用于部署站点文件，仓库名设置为用户名+.github.io ，https://Crush-hub.github.io即博客地址

 ## 4.博客部署到远端地址,生成public文件

```c#
hugo --theme=LoveIt --baseUrl="https://Crush-hub.github.io/" --buildDrafts
```

## 5.将public文件夹推送到github仓库

```c#
cd public

git init
git add .
git commit -m "yyyy/mm/dd-hh:mm"
git remote add origin https://github.com/Crush-hub/Crush-hub.github.io.git

git push -u origin master(第一次推送)

git push

git push -f
#强制更新
```

## 6.生成博客

```
https://crush-hub.github.io
```

# 引入图片

- 第一种方式：图片放置在根目录下的static中，也就是网站的绝对路径

```
![](/images/two_images.jpg)
```

弊端就是写博客时无法看到粘贴的图片

- 第二种方式：利用PicGo工具搭建图床，将gitee仓库设置为图床。

原理就是PicGo将图片上传到你的gitee仓库，然后返回给你图片的具体地址，这样你用该地址便可以访问到位于仓库的图片了。

## 1.下载安装PicGo

访问[PicGo release](https://github.com/Molunerfinn/PicGo/releases)下载操作系统对应安装包，注意不可安装到`C:\Program Files`，Typore无法解析该路径

## 2.安装npm

由于PicGo的插件需要使用npm进行安装，如果你的电脑上没有安装npm，那么无法安装PicGo插件，npm最低版本为6+

## 3.设置PicGo用Gitee作为图床

运行`PicGo`，单击`插件设置`，在搜索中输入`github`，安装搜索结果中的`github-plus`，如下图所示。

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721093138.png " ")

移步gitee并创建一个仓库，仓库名随意，但是必须设置为公开仓库且允许在线编辑，我创建的仓库地址是`https://gitee.com/cao-lianjie/pic-go`，创建完仓库后创建一个私人令牌，私人令牌是用来允许`PicGo`访问并更新你的仓库。

访问新建[私人令牌](https://gitee.com/profile/personal_access_tokens)PicGo要使用的私人令牌只需要`user_info`和`projects`权限，勾选上后提交，gitee将会返回私人令牌的`token`，保存该`token`，`token`只会出现一次，离开页面过后再不会出现。

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721094220.png " ")

回到Picgo，点击`图床设置->githubPlus`，在设置中填入`repo`和`token`，并选择`origin`为gitee，即可完成设置。

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721094429.png " ")

## 4. 设置Typora

使用PicGo有效避免了使用图片时候的`上传`->`编写markdown代码`的步骤，但是我们能不能把`添加到PicGo`这一步也省略掉呢？答案当然是可以，Typora内置了使用PicGo自动上传图片的功能，也就是说，在需要使用图片的时候，你只要直接将图片粘贴到Typora就好了，这样就跟使用本地图片的体验毫无差距了。

- 点击Typora左上角的`文件`->`偏好设置`
- 在弹出的界面中定位到`图像`，选择`插入图片时`选项为`上传图片`，并勾选`对网络位置的图片应用上述规则`
- 设置完成如图所示

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721100606.png " ")

- 选择`上传服务`为`PicGo(app)`，点击`验证图片上传选项`，如果出现如下图所示界面，说明配置已成功，然后你就可以直接在Typora中插入图片了，Typora会自动上传并替换图片地址为网络地址。

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721102610.png " ")

如出现以下错误,点击PicGo界面左侧的`PicGo设置`->`设置Server`，并按下图设置

```c#
Failed to fetch
```

![image-20210721102931206](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210721102931206.png " ")

# 新增文章

## 创建md文件

```
hugo new posts/FileName.md
```

## 本地测试

```
hugo server -t LoveIt --buildDrafts --disableFastRender
```

## 生成public文件

```
hugo --theme=LoveIt --baseUrl="https://Crush-hub.github.io/" --buildDrafts
```

## 推送到github

```
git add .
git commit -m "yyyy/mm/dd-hh:mm"
git push 
```



# Loveit主题配置问题



## 标签与分类参数

- LoveIt主题官方前置参数

```properties
---
title: "我的第一篇文章" 
		#文章标题
subtitle: ""
		#文章副标题
date: 2020-03-04T15:58:26+08:00
		#这篇文章创建的日期时间. 它通常是从文章的前置参数中的 date 字段获取的, 但是也可以在 网站配置 中设置.
lastmod: 2020-03-04T15:58:26+08:00
		#上次修改内容的日期时间
draft: true
		#如果设为 true, 除非 hugo 命令使用了 --buildDrafts/-D 参数, 这篇文章不会被渲染.
author: ""
		#文章作者
authorLink: ""
		#文章作者的链接
description: ""
		#文章内容的描述
license: ""
		#这篇文章特殊的许可
images: []
		#页面图片, 用于 Open Graph 和 Twitter Cards.
tags: []
		#文章的标签
categories: []
		#文章所属的类别
featuredImage: ""
		#文章的特色图片
featuredImagePreview: ""
		#用在主页预览的文章特色图片
hiddenFromHomePage: false
		#如果设为 true, 这篇文章将不会显示在主页上
hiddenFromSearch: false
		#如果设为 true, 这篇文章将不会显示在搜索结果中.
twemoji: false
		#如果设为 true, 这篇文章会使用 twemoji.
lightgallery: true
		#如果设为 true, 文章中的图片将可以按照画廊形式呈现.
ruby: true
		#如果设为 true, 这篇文章会使用 上标注释扩展语法.
fraction: true
		#如果设为 true, 这篇文章会使用 分数扩展语法
fontawesome: true
		#如果设为 true, 这篇文章会使用 Font Awesome 扩展语法.
linkToMarkdown: true
		#如果设为 true, 内容的页脚将显示指向原始 Markdown 文件的链接.
rssFullText: false
		#如果设为 true, 在 RSS 中将会显示全文内容.
		#toc: 和网站配置 中的 params.page.toc 部分相同.
		#code: 和网站配置 中的 params.page.code 部分相同.
		#math: 和网站配置 中的 params.page.math 部分相同.
		#mapbox: 和网站配置 中的 params.page.mapbox 部分相同.
		#share: 和 网站配置 中的 params.page.share 部分相同.
		#comment: 和网站配置 中的 params.page.comment 部分相同.
		#library: 和网站配置中的 params.page.library 部分相同.
		#seo: 和网站配置中的 params.page.seo 部分相同.

toc:
  enable: true
  auto: true
code:
  copy: true
  # ...
math:
  enable: true
  # ...
mapbox:
  accessToken: ""
  # ...
share:
  enable: true
  # ...
comment:
  enable: true
  # ...
library:
  css:
    # someCSS = "some.css"
    # 位于 "assets/"
    # 或者
    # someCSS = "https://cdn.example.com/some.css"
  js:
    # someJS = "some.js"
    # 位于 "assets/"
    # 或者
    # someJS = "https://cdn.example.com/some.js"
seo:
  images: []
  # ...
---

```

在博客根目录`archetypes`文件夹下设置`default.md`默认标签如下：

```properties
title: "{{ replace .TranslationBaseName "-" " " | title }}"   
subtitle: ""	#
date: {{ .Date }}
lastmod: {{ .Date }}
draft: false
toc:
  enable: true
weight: false
categories: [""]
tags: [""]
```

新增文章需设置`categories和tags`标签

## 添加友情链接 shortcodes

hugo在主目录下layouts没有模板文件时,会找到themes下的layouts文件夹内的模板文件进行渲染.

- 1. `LoveIt/layouts/shortcodes/` 下面新建 `friend.html` 文件：

  ```html
  {{ if .IsNamedParams }}
  <a target="_blank" href={{ .Get "url" }} title={{ .Get "name" }} class="friendurl">
    <div class="frienddiv">
      <div class="frienddivleft">
        <img class="myfriend" src={{ .Get "logo" }} />
      </div>
      <div class="frienddivright">
        <div class="friendname">{{ .Get "name" }}</div>
        <div class="friendinfo">{{ .Get "word" }}</div>
      </div>
    </div>
  </a>
  {{ end }}
  ```

- 2. `LoveIt/assets/css/_partial/_single/` 下面新建 `_friend.scss` 文件：

  ```scss
  .friendurl {
   text-decoration: none !important;
   color: black;
  }
  
  .myfriend {
   width: 56px !important;
   height: 56px !important;
   border-radius: 50%;
   border: 1px solid #ddd;
   padding: 2px;
   box-shadow: 1px 1px 1px rgba(0, 0, 0, 0.15);
   margin-top: 14px !important;
   margin-left: 14px !important;
   background-color: #fff;
  }
  
  .frienddiv {
   height: 92px;
   margin-top: 10px;
   width: 48%;
   display: inline-block !important;
   border-radius: 5px;
   background: rgba(255, 255, 255, 0.2);
   box-shadow: 4px 4px 2px 1px rgba(0, 0, 255, 0.2);
  }
  
  .frienddiv:hover {
   background: rgba(87, 142, 224, 0.15);
  }
  
  .frienddiv:hover .frienddivleft img {
   transition: 0.9s !important;
   -webkit-transition: 0.9s !important;
   -moz-transition: 0.9s !important;
   -o-transition: 0.9s !important;
   -ms-transition: 0.9s !important;
   transform: rotate(360deg) !important;
   -webkit-transform: rotate(360deg) !important;
   -moz-transform: rotate(360deg) !important;
   -o-transform: rotate(360deg) !important;
   -ms-transform: rotate(360deg) !important;
  }
  
  .frienddivleft {
   width: 92px;
   float: left;
  }
  
  .frienddivleft {
   margin-right: 2px;
  }
  
  .frienddivright {
   margin-top: 18px;
   margin-right: 18px;
  }
  
  .friendname {
   text-overflow: ellipsis;
   overflow: hidden;
   white-space: nowrap;
  }
  
  .friendinfo {
   text-overflow: ellipsis;
   overflow: hidden;
   white-space: nowrap;
  }
  
  @media screen and (max-width: 600px) {
   .friendinfo {
    display: none;
   }
   .frienddivleft {
    width: 84px;
    margin: auto;
   }
   .frienddivright {
    height: 100%;
    margin: auto;
    display: flex;
    align-items: center;
    justify-content: center;
   }
   .friendname {
    font-size: 14px;
   }
  }
  ```

- 3. `LoveIt/assets/css/_page/` 下面修改 `_single.scss`，引入下面一行：

  ```scss
  @import "../_partial/_single/friend";
  ```

- 4. `Myblog\content`目录下新建`friend`文件夹，文件夹内新建`index.语言.md`，配置如下：

  友链示例：

  ```scss
  {{（示例）< friend name="Dillon" url="https://github.com/dillonzq/" logo="https://avatars0.githubusercontent.com/u/30786232?s=460&u=5fc878f67c869ce6628cf65121b8d73e1733f941&v=4" word="LoveIt主题作者" >}}
  {{</* friend name="Z字骚年" url="https://zouyx.github.io/" logo="https://avatars.githubusercontent.com/u/3828072?v=4&s=160" word="Joe Zou's Blog" */>}}
  {{</* friend name="张其" url="https://blog.csdn.net/u010927340" logo="https://avatars3.githubusercontent.com/u/12484497?v=4&s=160" word="张其的博客" */>}}
  ```

  

  ```scss
  ---
  hiddenFromSearch: true
  ---
  {{</* friend name="Z字骚年" url="https://zouyx.github.io/" logo="https://avatars.githubusercontent.com/u/3828072?v=4&s=160" word="Joe Zou's Blog" */>}}
  {{</* friend name="张其" url="https://blog.csdn.net/u010927340" logo="https://avatars3.githubusercontent.com/u/12484497?v=4&s=160" word="张其的博客" */>}}
  ```

## 摘要分割符

添加摘要分割符来拆分文章生成摘要.摘要分隔符之前的内容将用作该文章的摘要.注意全部为小写且没有空格.

```
<!- -more- ->
```

## 注意和技巧代码框

插值表达式`< /admonition note/tip>`引入注意代码框/技巧框，示例如下：

```
< admonition note "怎样选择搜索引擎?" >
以下是两种搜索引擎的对比:

* `lunr`: 简单, 无需同步 `index.json`, 没有 `contentLength` 的限制, 但占用带宽大且性能低 (特别是中文需要一个较大的分词依赖库)
* `algolia`: 高性能并且占用带宽低, 但需要同步 `index.json` 且有 `contentLength` 的限制

{{< version 0.2.3 >}} 文章内容被 `h2` 和 `h3` HTML 标签切分来提高查询效果并且基本实现全文搜索.
`contentLength` 用来限制 `h2` 和 `h3` HTML 标签开头的内容部分的最大长度.
< /admonition >
```



![搜索引擎设置](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210723144219.png " ")



```
{< admonition tip "关于 algolia 的使用技巧" >
你需要上传 `index.json` 到 algolia 来激活搜索功能. 你可以使用浏览器来上传 `index.json` 文件但是一个自动化的脚本可能效果更好.
[Algolia Atomic](https://github.com/chrisdmacrae/atomic-algolia) 是一个不错的选择.
为了兼容 Hugo 的多语言模式, 你需要上传不同语言的 `index.json` 文件到对应的 algolia index, 例如 `zh-cn/index.json` 或 `fr/index.json`...
< /admonition >
```

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210723144604.png " ")

## 开启画廊效果

- 第一步配置文件设置`lightgallery = true`，默认前置参数可设置单篇文章是否开启画廊
- 第二步在 Markdown 语法图片链接后面加个空格和空串，如：

```http
![](https://gitee.com/xx/xx.png " ")
```

CMS：内容管理系统(Content Management System)

正因为内容的核心地位，所以今天建设网站的技术框架中**CMS**（内容管理系统）是最为流行的，因为你需要有一个系统不停的发布新的贴近用户的内容，而不是只有一个冰冷的5页的页面和一个电话。

SEO是英文 Search Engine Optimization 的缩写，中文意思“搜索引擎优化”。SEO是指在了解搜索引擎自然排名机制的基础上，对网站进行内部及外部的调整优化，改进网站在搜索引擎中的关键词自然排名，从而获得更多流量，最终达成品牌建设或者产品销售的目的。

不管是百度还是谷歌等百科网站，对于SEO解释都是大同小异，简单来说就是通过一定技术手段提高网站关键词搜索排名获取更多展示，然后从自然搜索结果获得更多网站流量的过程。



## 未解决问题

- 未设置站点统计
- 未设置评论系统

- Git actions 自动部署博客









