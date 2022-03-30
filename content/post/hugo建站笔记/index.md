---
title: "Hugo建站笔记"
date: 2022-03-30T12:02:20+08:00
draft: false
image: test.jpg
categories:
    - 博客
tags:
    - Hugo
---

## 1. 安装hugo

### 创建 github仓库
https://github.com/feiyang05/blog.git 用于存放hugo工作区
https://github.com/feiyang05/feiyang05.github.io.git 用于存放和发布站点页面

### 安装hugo
下载地址 https://github.com/gohugoio/hugo/releases  
下载 hugo_extended_0.96.0_Windows-64bit.zip 解压得到 hugo.exe

```
hugo new site blog 
cd blog
move ..\hugo.exe .
git init
git remote add origin https://github.com/feiyang05/blog.git
git add -A
git commit -m "hugo init"
git push -u origin master
```

### 安装主题
```
git submodule add https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack
move config.toml config.toml.bak
copy themes\hugo-theme-stack\exampleSite\config.yaml .
copy themes\hugo-theme-stack\assets .\assets
```
### 修改站点信息
``` 
baseurl: https://feiyang05.github.io/
DefaultContentLanguage: zh-cn
title: 我的小站
```
### 启动服务
```
hugo server
```
访问 http://localhost:1313/ 可以预览网站   

## 2. 发表文章
### 新建文章
```
hugo new post/helloworld/index.md
```
### 编辑文章  
draft: false 文章可见  
image 顶栏图  
```
---
title: "Helloworld"
date: 2022-03-30T15:04:03+08:00
draft: false
image: test.jpg
categories:
    - 博客
tags:
    - Test    
---

## 标题
正文  
BALABALA  

![test](test.jpg)
```
将 test.jpg 放入 index.md 同级目录下，可以直接显示图片。  
如果图片放在了下一级目录，例如img目录，则文章中图片地址需要替换成‘img/test.jpg’
## 3. 构建和推送
### 构建页面
```
hugo 
```
### 推送站点页面 
生成的页面位于 public 目录下  
```
cd public
git init
git remote add origin https://github.com/feiyang05/feiyang05.github.io.git
git add -A
git commit -m "first commit"
git push -u origin master
```
等待片刻部署完成  
访问 https://feiyang05.github.io/   

## 4. 更新文章
将测试文章关闭
```
draft: true
```
推送更新
```
hugo
cd public
git add -A
git commit -m "modify helloworld"
git push -u origin master
```

## 5. 评论功能

因为Stack主题上自带的评论区插件是 [Disqus](https://disqus.com/) ，国内无法访问，因此需要换成其他插件。这里使用 utterances：utterances是一款基于Github Issue的Github工具,优点主要是无广告、加载快、配置简单，轻量开源  
### 安装utterances
访问 https://github.com/apps/utterances 点击 Install按钮，选择Only select repositories - feiyang05/feiyang05.github.io
### 修改配置
修改 config.yaml ，将 disqusjs 改为 utterances
```
    comments:
        enabled: true
        provider: utterances

        disqusjs:
            shortname:
            apiUrl:
            apiKey:
            admin:
            adminLabel:

        utterances:
            repo: feiyang05/feiyang05.github.io
            issueTerm: title
            label: comment
```

参考文档：  
https://gohugo.io/getting-started/usage/
https://cyhour.com/1226/
https://cloud.tencent.com/developer/article/1787522