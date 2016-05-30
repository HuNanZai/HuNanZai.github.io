---
title: 快速简单的个人博客搭建
date: 2016-05-04 14:17:41
categories:
tags: [个人]
---

# 简介

- [Hexo][0]+[Github][1]
- [我的博客][2]

# 准备工作

## For Windows

下面这些东西是需要你提前准备好的:
```
Github账号:在线托管你的博客  

GitBash:同步你的博客改动到Github(一些有意思的主题包的下载)  

NodeJs:构建整个博客相关的框架(hexo包)

各种相关的技术包:markdown语法、ssh啊什么的- -
```

# 开工！

## 0x00 Github中创建{Username}.github.io的仓库
1. Github->Repositories—>new

2. Add {Username} repository

3. Save

4. Got the git location:  
  
	git@github.com/{Username}/{Username}.github.io  

## 0x01 NodeJs安装Hexo
```
	npm install hexo-cli -g
```

## 0x02 构建本地博客
1. 初始化  

	找到一个空文件夹TmpDir

2. 构建  
	在文件夹中打开命令窗口执行

	>```
		hexo init	
	>```

3. 效果检查  

	构建完成之后，继续在命令窗口执行

	>```
		hexo server
	>```

	访问[http://localhost:4000/](http://localhost:4000/)遍可以看到自己的博客了！

4. 新建博文  

	执行命令

	>```
		hex new "xxx"
	>```
	
	可以看到生成了source/_posts/xxx.md,编辑对应的文件即可

## 0x03 发布
通过0x02你已经写好了自己的博文，怎么发布呢？

1. 通过git-bash生成自己的ssh->id_rsa.pub
	>```
	ssh-keygen -C "xxx@xxx.com"
	>```
2. 添加公钥到github-[ssh管理](https://github.com/settings/ssh)中

3. 修改博客根目录下的_config.yml  

	具体是关于Delpoy配置段

	<code>#Deployment</code><br>
	<code>##Docs: https://hexo.io/docs/deployment.html </code><br>
	<code>deploy:</code><br>
	<code>	type:git</code><br>
	<code>	repository: git@github.com:{Username}/{Username}.github.io.git</code><br>

4. 命令行安装hexo-deployer-git  

	>```
	npm install hexo-deployer-git --save
	>```

5. 部署上线！
	>```
	hexo deploy
	>```

## 0x04 访问http(s)://{Username}.github.io 来查看自己的博客！

[0]: https://hexo.io/zh-cn/
[1]: http://github.com/
[2]: http://hunanzai.github.io/