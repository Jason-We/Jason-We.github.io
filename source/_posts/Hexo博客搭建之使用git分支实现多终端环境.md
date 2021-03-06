---
title: Hexo博客搭建之使用git分支实现多终端环境
date: 2020-10-19 17:21:55
categories: hexo
tags:
  - hexo
  - git
  - 博客搭建
---

## 问题

> 该文前提默认你已经使用hexo在GitHub上搭建起了自己的博客系统，强烈建议先搭建好博客再读此文！

如果你现在在自己的笔记本上写的博客，部署在了网站上，那么你在家里用台式机，或者实验室的台式机，发现你电脑里面没有博客的文件，或者要换电脑了，最后不知道怎么移动文件，怎么办？

在这里我们就可以利用git的分支系统进行多终端工作了，这样每次打开不一样的电脑，只需要进行简单的配置和在github上把文件同步下来，就可以无缝操作了。

## hexo机制

由于`hexo d`上传部署到github的其实是hexo编译后的文件，是用来生成网页的，不包含源文件。

也就是上传的是在本地目录里自动生成的`.deploy_git`里面。

其他文件 ，包括我们写在source 里面的，和配置文件，主题文件，都没有上传到github

所以可以利用git的分支管理，将源文件上传到github的另一个分支即可。

## 具体操作

### 新建分支

首先在你的github pages项目仓库（如我的是[Jason-We.github.io](https://github.com/Jason-We/Jason-We.github.io)新建一个分支，名称自拟，可以是hexo。

然后在这个仓库的settings中，选择默认分支为hexo（这样每次同步的时候就不用指定分支，比较方便）。

### 本地克隆

在本地的任意你喜欢的目录下，将上述仓库克隆下来，因为默认分支已经设成了hexo，所以clone时只clone了hexo。接下来在克隆到本地的`ZJUFangzh.github.io`中，把除了.git 文件夹外的所有文件都删掉

把之前我们写的博客源文件全部复制过来，除了`.deploy_git`。这里应该说一句，复制过来的源文件应该有一个`.gitignore`，用来忽略一些不需要的文件，如果没有的话，自己新建一个，在里面写上如下，表示这些类型文件不需要git：

```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```

**注意，如果你之前克隆过theme中的主题文件，那么应该把主题文件中的`.git`文件夹删掉，因为git不能嵌套上传，最好是显示隐藏文件，检查一下有没有，否则上传的时候会出错，导致你的主题文件无法上传，这样你的配置在别的电脑上就用不了了。**

然后，

```
git add .
git commit –m "add branch"
git push 
```

这样就上传完了，可以去你的github上看一看hexo分支有没有上传上去，其中`node_modules`、`public`、`db.json`已经被忽略掉了，没有关系，不需要上传的，因为在别的电脑上需要重新输入命令安装 。

### 换电脑操作

在你已经安装好了git、nodejs、hexo的机器上，再任意你喜欢的空文件夹下，将你上述push好的的仓库克隆到本机。进入到该目录后，执行：

```
npm install
npm install hexo-deployer-git --save
```

之后 ， 生成+部署：

```
hexo g
hexo d
```

至此，已经搞定啦。接下来就可以在这台机器上愉快的写博客了。

```
hexo new "你的文章名称"
```

## Tips

1. 不要忘了，每次写完最好都把源文件上传一下

```
git add .
git commit –m "xxxx"
git push 
123
```

1. 如果是在已经编辑过的电脑上，已经有clone文件夹了，那么，每次只要和远端同步一下就行了

```
git pull
```