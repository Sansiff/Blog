---
title: Tmux
typora-root-url: tmux
date: 2022-07-05 10:20:11
categories: Linux
tags: Linux
---

## 会话与进程
命令行的典型使用方式是，打开一个终端窗口(terminal window，以下简称"窗口")，在里面输入命令。用户与计算机的这种临时的交互，称为一次"会话"(session) 。
会话的一个重要特点是，窗口与其中启动的进程是连在一起的。打开窗口，会话开始；关闭窗口，会话结束，会话内部的进程也会随之终止，不管有没有运行完。
一个典型的例子就是，SSH 登录远程计算机，打开一个远程窗口执行命令。这时，网络突然断线，再次登录的时候，是找不回上一次执行的命令的。因为上一次 SSH 会话已经终止了，里面的进程也随之消失了。
为了解决这个问题，会话与窗口可以"解绑"：窗口关闭时，会话并不终止，而是继续运行，等到以后需要的时候，再让会话"绑定"其他窗口。

## Tmux 的作用
Tmux 是一个终端复用工具：
- Tmux 支持在单个窗口中，同时访问多个会话；
- Tmux 支持新窗口"接入"已经存在的会话；
- Tmux 支持每个会话有多个连接窗口
- Tmux 支持窗口任意的垂直和水平拆分

## Tmux 的基本结构
Tmux 的结构包括会话(session)，窗口(window)，窗格(pane)三个部分。
会话的本质是伪终端的集合，每个窗格表示一个伪终端，多个窗格展现在一个屏幕上，这一屏幕就叫窗口。
在 Tmux 中，你可以创建多个会话(session)，每个会话会默认创建一个窗口，而每个窗口(window)又会默认创建一个窗格(pane),每个窗格都对应一个伪终端用于执行命令。简单来讲可以把它们看成是分组的关系，每个组内可以有多个终端用来执行命令。

## 会话管理

### 新建会话
第一个启动的 Tmux 会话会默认命名为0，第二个为1
```sh
tmux
```

```sh
tmux new-session <session-name>
# or
tmux new -s <session-name>
```

### 查看会话
```sh
tmux ls
# or
tmux list-session
```

### 接入会话
```sh
tmux attach -t <session-name>
```


### 切换会话
```sh
tmux switch -t <session-name>

# or 列出所有会话切换
Ctrl+b s
```

### 退出当前的会话
```sh
tmux detach
# or
Ctrl+b d
```
tmux detach 执行后就会退出当前的会话，但是会话不会结束，仍在后台运行

### 杀掉会话
```sh
tmux kill-session -t <session-name>
```

### 重命名会话
```sh
tmux rename-session -t <session-name> <new-session-name>

# or 重命名当前会话
Ctrl+b $ 
```

## 窗口管理
Tmux 的会话里可以有多个窗口，一下命令都是在 session 中运行

### 新建窗口
```sh
tmux new-window

# 指定名称
tmux new-window -n <window-name>
```

### 切换窗口
```sh
tmux select-window -t <window-name>

# or 列出所有窗口切换
Ctrl+b w
```

### 杀掉窗口
```sh
tmux kill-window -t <window-name>
```

### 重命名窗口
```sh
tmux rename-window -t <window-name> <new-window-name>

# 修改当前窗口
tmux rename-window <new-window-name>
```

## 窗格操作
Tmux 可以将窗口分成多个窗格，每个窗格运行不同的命令。以下命令都是在 Tmux 窗口中执行。
这里只写一些常用的快捷键
```sh
# 划分左右两个窗格
Ctrl+b %     

# 划分上下两个窗格
Ctrl+b "     

# 光标切换窗格
Ctrl+b <arrow key> 

# 关闭当前窗格
Ctrl+b x

# 将当前窗格拆分为一个独立窗口
Ctrl+b !

# 将当前窗格全屏显示，再使用一次会变回原来大小
Ctrl+b z

# 按箭头方向调整窗格大小
Ctrl+b Ctrl+<arrow key>

# 显示窗格编号
Ctrl+b q
```

## 其他操作
```sh
# 列出所有快捷键，及其对应的 Tmux 命令
tmux list-keys

# 列出所有 Tmux 命令及其参数
tmux list-commands

# 列出当前所有 Tmux 会话的信息
tmux info

# 重新加载当前的 Tmux 配置
tmux source-file ~/.tmux.conf
```
