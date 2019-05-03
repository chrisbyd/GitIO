---
title: Scala Cats
date: 2019-04-28 00:23:30
tags:
---

# Scala Cats 初探

![Cats logo](http://plastic-idolatry.com/erik/cats2.png)

这次准备通过看一些厉害的包，学习Scala的语法。Scala Cats是用途非常广泛的一个包，提供了许多Type Class。将一一解构一下。



## Kernel

**Kernel** 是 Cats包里最为基础的一个部分。它主要提供了非常有用的几个Type Class.



| Type Class |  父类 | 特征 | 说明 | 实例 |
|:------------- |:---------------:| -------------:| :---: | :---:|
| SemiGroup    | Any |     combine: a->a->a    |  半群满足结合律 | String上的append运算满足半群， Int上的+或者乘法也满足半群
| Monoid      | SemiGroup        |   增加 empty: a  | 幺半群，幺代表有幺元，任意半群中元素和它结合依然是自己 | String 上的空字符串，Int上加法的zero，乘法的1都是对应群的幺元 |
| Group | Monoid      |   增加逆元 inverse: a->a   | 群满足四个要素，其中封闭性显然满足，半群提供结合律，Monoid提供幺元，自己提供逆元 | 整数加法群的相反数，乘法群的倒数 |
| Band | SemiGroup      |   增加幂等约束   | 对于任何半群中元素xx=x，乘法表示的是群中的运算 | 布尔环,true and true is true, false and false is false |
|  Commutative[Group/SemiGroup/Monoid] | [Group/SemiGroup/Monoid]    |   增加交换律约束  | 显然很多运算都满足交换律 | 整数加法群乘法满足交换律，String Append不满足 |
|  Semilattice | Band，CommutativeSemigroup    |   有结合律 (xy)z=x(yz);交换律 xy=yx；有蜜等xx=x  | 半格, 用来引出偏序关系，x<=y定义为xy=x，显然x<=x因为xx=x，显然x<=y<=z=>x<=z,因为xyyz=xyz=xz=xyy=x, 显然x<=y,y<=x=>x=y，因为xy=x=yx=y | Bool上的and 运算|
|  Bounded Semilattice | Semilattice，CommutativeMonoid    |   有幺元有最大/最小值  | 用来引出全序关系， 显然x1=x 存在最小值| Bool上的and 运算|

> 然后引出 Eq => Partial Order => Order


