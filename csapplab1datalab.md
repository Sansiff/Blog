---
title: csapplab1datalab
typora-root-url: csapplab1datalab
date: 2024-06-06 18:58:30
categories: CSAPP
tags: CSAPP
---

## 说明

datalab主要是提供了一系列puzzle，限制使用的操作符号来实现对应的函数

一些说明：

1. 初始化整型参数时使用的整型常量的范围是$[0,255$(0xFF)$]$
2. 只允许使用局部变量（不允许使用全局变量）
3. 一元操作符 ! ~
4. 二元操作符 & ^ | + << >>

不允许的操作：

1. 使用任何条件控制语句
2. 定义和使用宏
3. 定义其他的函数
4. 调用函数
5. 使用其他操作符
6. 使用类型转换
7. 使用除int之外的类型

可以假设机器的类型是

1. 使用2's complent，32位
2. 执行算术右移
3. 移动超过字长的位数会出问题

## tools

使用dlc来检测代码是否符合要求

```shell
./dlc bits.c
# -e 检查运行次数
./dlc -e bits.c
```

使用BDD checker来检查代码是否正确

```shell
make btest
./btest
# -f <name> 单独测试 named function
./btest -f tmin
```

使用ishow和fshow来查看int和float的表示状态

```shell
make 
./ishow 20
./ishow 0x3f3f3f3f
```

## bitXor

使用&和~来实现^操作

主要是对De Morgan's laws的应用：

考虑到$x \oplus y = (x \and \lnot y) \lor (\lnot x \and y) = \lnot(\lnot(x \and \lnot y) \lor (\lnot x \and y)) = \lnot(\lnot(x \and \lnot y) \and \lnot(\lnot x \and y))$

也可以通过$x \oplus y = \lnot((x \and y) \lor (\lnot x \and \lnot y)) = \lnot(x \and y) \and \lnot (\lnot x \and \lnot y)$

```c
/* 
 * bitXor - x^y using only ~ and & 
 *   Example: bitXor(4, 5) = 1
 *   Legal ops: ~ &
 *   Max ops: 14
 *   Rating: 1
 */
int bitXor(int x, int y) {
  return ~(x&y)&~(~x&~y);
}
```

## tmin

```c
/* 
 * tmin - return minimum two's complement integer 
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 4
 *   Rating: 1
 */
int tmin(void) {
  return 1<<31;
}
```

## isTmax

Hint

1. $T_{max} + 1 = T_{min}$
2. $T_{max} \oplus T_{min} = -1$
3. $\sim (-1) = 0$

```c
/*
 * isTmax - returns 1 if x is the maximum, two's complement number,
 *     and 0 otherwise 
 *   Legal ops: ! ~ & ^ | +
 *   Max ops: 10
 *   Rating: 1
 */ 
int isTmax(int x) {
  return !~((x + 1) ^ x) & !!(x + 1) ;
}
```

## allOddBits

考虑

```c
/* 
 * allOddBits - return 1 if all odd-numbered bits in word set to 1
 *   where bits are numbered from 0 (least significant) to 31 (most significant)
 *   Examples allOddBits(0xFFFFFFFD) = 0, allOddBits(0xAAAAAAAA) = 1
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 12
 *   Rating: 2
 */
int allOddBits(int x) {
  return !((x & 0xAAAAAAAA) ^ 0xAAAAAAAA);
}
```

## negate

Hint

1. $A + \sim A = -1$
2. $-A = \sim A + 1$

```c
/* 
 * negate - return -x 
 *   Example: negate(1) = -1.
 *   Legal ops: ! ~ & ^ | + << >>
 *   Max ops: 5
 *   Rating: 2
 */
int negate(int x) {
  return ~x + 1;
}
```

