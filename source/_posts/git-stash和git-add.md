---
title: git stash和git add
date: 2019-08-12 15:50:03
tags: "Git"
---

## git stash 常用命令:

1. git stash save "save message" : 执行存储时，添加备注，方便查找，只有 git stash 也要可以的，但查找时不方便识别。

2. git stash list ：查看 stash 了哪些存储

3. git stash show ：显示做了哪些改动，默认 show 第一个存储,如果要显示其他存贮，后面加 stash@{\$num}，比如第二个 git stash show stash@{1}

4. git stash show -p : 显示第一个存储的改动，如果想显示其他存存储，命令：git stash show stash@{\$num} -p ，比如第二个：git stash show stash@{1} -p
<!-- more -->
5. git stash apply :应用某个存储,但不会把存储从存储列表中删除，默认使用第一个存储,即 stash@{0}，如果要使用其他个，git stash apply stash@{\$num} ， 比如第二个：git stash apply stash@{1}

6. git stash pop ：命令恢复之前缓存的工作目录，将缓存堆栈中的对应 stash 删除，并将对应修改应用到当前的工作目录下,默认为第一个 stash,即 stash@{0}，如果要应用并删除其他 stash，命令：git stash pop stash@{\$num} ，比如应用并删除第二个：git stash pop stash@{1}

7. git stash drop stash@{$num} ：丢弃stash@{$num}存储，从列表中删除这个存储

8. git stash clear ：删除所有缓存的 stash

- 说明:<font color=red >新增的文件，直接执行 stash 是不会被存储的,如果要保存这个新增的文件,需要先执行下 git add 把文件加到 git 版本控制中，然后再 git stash 就可以了</font>

- 总结下：<font color=red >git add 只是把文件加到 git 版本控制里，并不等于就被 stash 起来了，git add 和 git stash 没有必然的关系，但是执行 git stash 能正确存储的前提是文件必须在 git 版本控制中才行。</font>

* 常规 git stash 的一个限制是它会一下暂存所有的文件。有时，只备份某些文件更为方便，让另外一些与代码库保持一致。一个非常有用的技巧，用来备份部分文件：

1. add 那些你不想备份的文件（例如： git add file1.js, file2.js）
2. 调用 git stash –keep-index。只会备份那些没有被 add 的文件。
3. 调用 git reset 取消已经 add 的文件的备份，继续自己的工作。
