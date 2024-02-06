---
title: PicGo+VSCode+Github
tags:
  - Github
  - PicGo
  - 工具
categories:
  - 折腾
  - 图床
keywords: 图床,PicGo
cover: https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/PicGo_logo.png
date: 2023-10-20 22:09:00
updated: 2023-11-15 00:00:00
description:
top_img:
comments:
katex:
---

VSCode 中有一个插件 PicGo 还算好用，可以一键将图片上传然后将链接粘贴到 Markdown 中。

写博客的时候直接把 Markdown 的相对地址贴在对应项目里，然后通过相对链接访问，使用的时候发现一些问题：

- 项目的相对路径未必是上传后的真实路径，导致每次都要手动编辑地址。比如我的 Blog 中的上传图片的地址是 /public/image，但 public 到了发布时会被 copy 到根路径，此时自动生成的相对地址就不匹配了。

于是使用 PicGo 中提供的图床功能将图片放到 GitHub 图床就不用担心图片链接错误了。

# 在Github中新建一个仓库来作为图床

## 创建仓库


![](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20230830191759.png)

仓库名称自定义，一定要选择公开仓库。

## 设置token，保留后续使用

进入github设置，点击左侧选项中最后一个 Developer settings

![](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20230830193013.png)

之后选择Personal access tokens下拉菜单中的Tokens

![](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20230830193102.png)
Generate new token(classic)

![](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20230830193414.png)

填写note，选择过期时间，可以选择最后一项，永久有效。下方选项框，只需要勾选repo

点击页面下方的Generate token

生成一串token，注意token只会显示一次，复制下来记到备忘录
![](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20230830194212.png)

# 下载PicGo

## PicGo(app)

访问PicGo官方文档[下载安装页面](https://picgo.github.io/PicGo-Doc/zh/guide/#%E4%B8%8B%E8%BD%BD%E5%AE%89%E8%A3%85)
![下载界面](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/202311131835010.png)

选择一个下载源安装即可

完成安装后，在PicGo（app）中配置github
![alt text](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/202311131838063.png)
github网络国内经常无法访问，如有必要，在picgo设置中设置代理
https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/202311161537187.png

## PicGo-core

PicGo-core没有图形界面，使用命令执行，更适合linux系统

进入[picgo官方文档](https://picgo.github.io/PicGo-Core-Doc/zh/guide/)

![](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20240206201059.png)

建议选择“全局安装”，执行以下命令：
```bash
# 安装
yarn global add picgo # 或者 npm install picgo -g
```


安装成功后在命令行输入

`picgo -v  #查看当前安装版本`

![](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20240206201404.png)

出现版本号说明安装成功

配置config

选择自动生成

通常来说你只需要配置 Uploader 即可，所以你可以通过 picgo set uploader 来进入交互式命令行，配置成功后会自动生成配置文件，无需复制粘贴！其他更多的命令可以参考 [CLI 命令](https://picgo.github.io/PicGo-Core-Doc/zh/guide/commands.html) 一章。

![alt text](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/image-20231113184359863.png)
注意

同时，填好图床配置之后，请务必通过 picgo use uploader 选择当前要使用的 Uploader。

# VSCode中配置PiCgo插件

## 下载Picgo插件

![alt text](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20230831162010.png)

点击安装即可

## 设置Picgo

![alt text](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20230831161045.png)

下拉找到Github相关的设置，只需要填写这一部分即可

![alt text](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20230831161313.png)

与上面一样：

- Current选择Github

- Branch分支一般默认就填main

- Custom Url是图片的访问地址，不填为默认地址，不过github在国内被墙，默认地址需要开梯子才能访问到。这里使用cdn加速，填写https://cdn.jsdelivr.net/gh/你的github用户名/仓库名

- Path是仓库中的文件夹名

- Repo填你的用户名/仓库名

- 最后Token填写上面我们复制的Token
至此，所有配置都已完成

# 完成测试

## VSCode中

可以截图在VSCode中用快捷键“Ctrl+Alt+U”来测试是否成功

配置没出错上传图片会弹出如下提示

![alt text](https://cdn.jsdelivr.net/gh/TRAVISZHAN/images/blog/20230831162724.png)

## 在app中

直接拖拽或者粘贴文件就可以进行图片上传

