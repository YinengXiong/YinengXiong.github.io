---
layout:     post
title:      "Build Personal Blog with Github & Jekyll"
subtitle:   " "
date:       2017-08-02
author:     "Yineng Xiong"
header-img: "img/2017-08-02.jpg"
tags:
    - Github
    - Jekyll
---

> Shape of 哇!



## Requirement
* Github
* Jekyll

1. [Github Pages](https://github.com/) is where people build software. After registration,  [create a new repository](https://github.com/new). The name of repo should corresponding with Gighub account, like `***.github.io`

2. [Jekyll](http://jekyllrb.com/) is a website generator that's designed for building minimal, static blogs to be hosted on Github Pages. [Jekyll中文网站](http://jekyll.com.cn/)
## Choose your favourite theme

[Jekyll Themes](http://jekyllthemes.org/)<br>
Mine is [here](https://github.com/huxpro/huxpro.github.io/)

## Domain Registration

1. [万网注册域名](https://wanwang.aliyun.com/)

2. Go to the root of your blog's repo and edit the **CNAME** file to include your domain name (e.g. `yinengxiong.cn`)

3. Go to your domain name registrar and add **CNAME DNS** record pointing your domian to Github Pages

## Write Posts

Feel free to checkout **Markdown** files in the `_posts/`

The **front-matter** of a post should like:

```Shell
---
layout:     post
title:      "Hello"
subtitle:   "Hello"
date:       2017-08-22 14:00:00
author:     "Yineng Xiong"
header-img: "img/your-mum.jpg"
tags:
    - Alibaba
---
```

## Submit

Just `git push`

## Current function

* Comment (Using [Disqus](http://www.disqus.com/), 需要翻墙)
* Tags search
* Baidu Analytics
* Google Analytics
* Links
* [Twitter](https://twitter.com/YinengXiong), [知乎](https://www.zhihu.com/people/YinengXiong), [Weibo](http://weibo.com/yinengxiong), [Facebook](https://www.facebook.com/yinengxiong), [Github](https://github.com/YinengXiong) pages

## Finally
Aha!
