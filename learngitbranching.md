---
title: Learn Git Branching
typora-root-url: learngitbranching
date: 2023-10-09 19:14:05
categories: git
tags: git
---
## 基础篇

### Git Commit

```shell
git commit
git commit
```

### GIt Branch

```shell
git checkout -b bugFix
```

### Git Merge

```shell
git checkout -b bugFix
git commit
git checkout main
git commit
git merge bugFix
```

### Git Rebase

```shell
git checkout -b bugFix
git commit
git checkout main
git commit
git checkout bugFix
git rebase main
```

## 高级篇

### 分离 Head

```shell
git checkout c4
```

### 相对引用

```shell
git checkout c3
```

### 相对引用2

```shell
git branch -f main c6
git checkout bugFix~2
git branch -f bugFix HEAD^
```

### 撤销变更

