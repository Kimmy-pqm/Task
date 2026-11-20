# Git
看廖雪峰老师的教程后整理如下笔记
***

## 一、Git是什么东西
目前世界上最先进的分布式版本控制系统！
同时可以帮助我们自动记录每次文件的改动
还可以和伙伴一起协作编辑

## 二、Git的诞生
Linus手搓不动所有人的代码了然后为了使用一个免费的版本控制系统，自己用C搓了一个Git出来……


>### ==当时免费的版本控制系统也有 Linus为啥不用呢？==
>#### 1.集中式版本控制器
>![集中式版本控制器运行示意图](http://cdn.jsdeliver.net/gh/Kimmy-pqm/img-bed/images/20261120150225402.jpg)
一切版本都得从这个中央控制器出或者进，程序上很多，就导致处理的很慢！还得联网才能工作，这样子就很局限。
eg.CVS SVN

>#### 2.分布式版本控制器
>没有那个中央控制器，版本库在各自的电脑里

## 三、配置Git和创建版本库
### 1.配置Git
```Git
$ git config --global user.name "your name"
$ git config --global user.email "email@example.com"
```

### 2.创建版本库 （在Git仓库内执行）
#### (1)将文件加入到仓库中(多次提交不同文件)
```Git
$ git add hello.md
```

#### (2)把文件提交到仓库（一次提交多个文件）
```Git
$ git commit -m "wrote a hello file"
```

#### (3)告诉你仓库是否被修改过
```Git
$ git status
```

#### (4)查找修改内容
```Git
$ git status
```

#### (5)修改日志
```Git
$ git log
```
>嫌输出信息太多？
>```Git
>$ git log --pretty=oneline
>```
>假如输出内容有一大串数字——commit ID

#### (6)版本回退
##### a.前情提要
HEAD 代表当前版本
HEAD^ 代表上一个版本
以此类推
==（不麻烦写法）== HEAD~100 代表上一百个版本

##### b.回退指令
```Git
$ git reset --hard HEAD^
```
>注意区分：
>>--hard会回退到上个版本的已提交状态(争取掌握这个！)
--soft会回退到上个版本的未提交状态
--mixed会回退到上个版本已添加但未提交的状态

#### （7）查找命令历史——commit ID
```Git
$ git relog
```

## 四、工作区与暂存区
（暂缓 后续学）

## 五、远程仓库



