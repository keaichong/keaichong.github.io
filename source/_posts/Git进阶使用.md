---
title: Git进阶使用
date: 2019-02-14 18:19:40
tags: Git
---

# Git 进阶操作

## 查看历史

在多次提交之后，本地仓库中就有了多个版本，如何查看历史版本呢？在 Git bash 中输入如下命令：

```bash
$ git log
```

结果如下图：
{% asset_img 3C2240A2-B575-4674-A941-B575BFD96F08.png  %}

说明：

每次提交都会有一个 SHA-1 **校验和(唯一标识)**、**作者的名字**和**电子邮件地址**、**提交时间**，最后缩进一个段落显示**提交说明**。

> 提示：如果提交次数太多，一屏显示不了，最后一行会显示: 表示未显示全，按键盘上的**Q 键**，可以显示下一页

可以通过`git log`的参数设置历史提交的展示方式，当历史提交数过多的时候可以使用如下命令：

```bash
$ git log --pretty=oneline
```
<!-- more -->
## 撤销操作

有了 Git，你就可以吃后悔药了，代码出问题，你可以恢复到之前的某个版本继续开发。任何时候，你都有可以撤消刚才所做的某些操作。

### 回退到某个版本

```bash
$ git reset --hard commit_id(校验和)
```

commit_id(校验和)不用写全，只写**前几位**即可，有了此命令就可以在历史记录里穿梭。HEAD 是指向当前版本的一个指针，使用`git reset`其实是改变 HEAD 指针，指向指定的版本。

> 注意：使用此命令可以还原到指定的版本，当前项目中未提交的内容就无法还原。

### reflog

假设有 5 个版本，你回退到第 4 个版本后，第 5 个版本就不存在了(使用`git log`查看)，此时想要回到第 5 个版本就需要知道第 5 个版本的 commit_id，如何找到这个 commit_id 呢？

```bash
$ git reflog
```

> 使用`git reflog`可以查看所有的所有操作记录。

### 检出指定文件

当某个文件修改出现问题，可以通过`git checkout`还原到最后一次提交。

```bash
$ git checkout -- file.js
```

通过上面的命令可以把 file.js 撤销到最后一次提交(最近提交的版本)

### 小结

| 序号 | 命令                           | 功能                   |
| ---- | ------------------------------ | ---------------------- |
| 01   | **git log**                    | 查看历史版本           |
| 02   | **git log --pretty=oneline**   | 以更方便的方式查看历史 |
| 03   | **git reset --hard commit_id** | 回退到指定版本         |
| 04   | **git reflog**                 | 查看所有的操作记录     |
| 05   | **git checkout -- file.js**    | 检出指定文件           |

## 分支操作

当我们使用 Git 第一次提交的时候其实就已经有了一个默认的分支 master。

### 什么时候需要使用分支？

- 开发新特性(feature 分支)
- 正在开发的过程中继续修改一个 bug(bugfix 分支)
- 为了保证 master 分支的稳定性，创建 dev 分支

### 常用分支命令

#### **查看分支**

```bash
$ git branch
```

#### **新建分支**

新建分支会基于当前分支当前版本，新建一个分支(内容和当前分支一样)

```bash
$ git branch testing
```

{% asset_img branch-01.png  %}

当有多个分支的时候，Git 如何知道我们当前在哪个分支工作呢？Git 保存着一个名为**HEAD 的指针**，该指针指向**当前工作的分支**。如下图：

{% asset_img branch-02.png  %}

使用`git branch'命令可以看到当前所有的分支，和当前工作的分支(前面加\*号的分支)，如下图：

{% asset_img image-201803182313451.png  %}

#### 切换分支

假设 testing 是开发分支，我们如何切换到开发分支呢？

```bash
$ git checkout testing
```

此时切换到 testing 分支，可以开心的在当前分支工作了。

{% asset_img branch-03.png  %}

新建和合并分支可以简化为：

```bash
$ git checkout -b testing
```

相当于下面两个命令

```bash
$ git branch testing
$ git checkout testing
```

#### testing 分支提交

```bash
# 修改某个文件
$ git commit -m '修改内容'
```

每次提交后 HEAD 随着分支一起向前移动

{% asset_img branch-04.png  %}

#### 合并分支

当在 testing 分支某个功能开发完毕后，需要把内容合并到 master 分支，此时需要两步：

1. 切换到 master 分支

   ```bash
   $ git checkout master
   ```

2. 把 testing 的修改合并到 master 分支

   ```bash
   $ git merge testing
   ```

   当合并完毕，master 和 testing 分支同时指向 c2b9e 这次提交

{% asset_img branch-05.png  %}

### 小结

| 序号 | 命令                        | 功能           |
| ---- | --------------------------- | -------------- |
| 01   | **git branch**              | 查看分支       |
| 02   | **git branch testing**      | 新建分支       |
| 03   | **git checkout testing**    | 切换分支       |
| 04   | **git checkout -b testing** | 新建和合并分支 |
| 05   | **git merge testing**       | 合并分支       |
