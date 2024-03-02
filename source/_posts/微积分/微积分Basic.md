---
title: 微积分：必须掌握的前置知识
tags:
  - 微积分
categories:
  - 微积分
  - 灌输知识
abbrlink: 7ca53540
date: 2024-03-02 10:00:00
cover: https://p.wzsco.top/c16e11102c0bbbec65a1949ceaf9b4e0.png/cover
---

## 函数

1. 定义：函数 $f(x)$ 是一种将输入值 $x$ 映射到输出值 $y=f(x)$ 的规则。
2. 图像：函数 $f(x)$ 在平面直角坐标系中的图像是由所有满足 $y=f(x)$ 的点 $(x,y)$ 构成的集合。
3. 性质：函数可以是奇函数或偶函数，也可以是周期函数或非周期函数，还可以是单调函数或非单调函数。

## 极限

1. 定义：当自变量 $x$ 趋近于某个值（可能是有限的或无限的），函数 $f(x)$ 的取值也随之趋近于某个值 $L$ 时，称 $L$ 是函数 $f(x)$
   当 $x$ 趋近于该值时的极限，记作 $\lim\limits_{x\to a}f(x)=L$。
2. 性质：
    1. 唯一性：如果 $\lim\limits_{x\to a}f(x)$ 存在，则极限唯一；
    2. 局部有界性：如果 $\lim\limits_{x\to a}f(x)=L$，则存在一个邻域 $N(a,\delta)$，使得 $f(x)$ 在这个邻域内有界；
    3. 夹逼定理：如果 $g(x)\leq f(x)\leq h(x)$，并且 $\lim\limits_{x\to a}g(x)=\lim\limits_{x\to a}h(x)=L$，则
       $\lim\limits_{x\to a}f(x)=L$。

## 导数

1. 定义：函数 $f(x)$ 在点 $x_0$ 处的导数是函数在该点处的切线斜率。记作 $f'(x_0)=\lim\limits_{\Delta x\to 0}\frac{f(
   x_0+\Delta x)-f(x_0)}{\Delta x}$ 或者 $\frac{dy}{dx}$。
2. 性质：
    1. 和法，则 $(u\pm v)'=u'\pm v'$；
    2. 积法，则 $(uv)'=u'v+uv'$；
    3. 商法，则 $\left(\frac{u}{v}\right)'=\frac{u'v-uv'}{v^2}$；
    4. 链式法则，则 $(f(g(x)))'=f'(g(x))g'(x)$。

## 积分

1. 定义：积分是求解曲线下面围成的面积的一种方法。对于定义在区间 $[a,b]$ 上的非负连续函数 $f(x)$，可以将 $[a,b]$ 分成 $n$
   个小区间，并取每个小区间中任意一点 $x_i$，其中 $i=1,2,\cdots,n$。然后作出下列和式：$S=\sum_{i=1}^n f(x_i)\Delta x$，其中
   $\Delta x=\frac{b-a}{n}$，并令 $n\to\infty$，则当极限存在时，该极限值称为函数 $f(x)$ 在区间 $[a,b]$ 上的定积分，记作
   $\int_a^b f(x)dx$。
2. 性质：
    1. 积分第一中值定理：如果函数 $f(x)$ 在区间 $[a,b]$ 上连续，则存在一个点 $c\in[a,b]$，使得 $\int_a^b f(x)dx=f(c)(b-a)$；
    2. 变量代换：设变换 $y=g(x)$ 具有连续导数，且其反函数 $x=h(y)$ 也具有连续导数，则有 $\int_a^b f(g(x))g'(x)dx=\int_{g(a)
       }^{g(b)} f(u)du$，其中 $u=g(x)$；
    3. 分部积分：$\int u dv=uv-\int v du$；
3. 常用积分公式：
    1. $\int x^ndx=\frac{x^{n+1}}{n+1}+C$
    2. $\int \frac{1}{x}dx=\ln|x|+C$
    3. $\int e^xdx=e^x+C$
    4. $\int \sin x dx=-\cos x+C$
    5. $\int \cos x dx=\sin x+C$
    6. $\int \tan x dx=-\ln|\cos x|+C$
    7. $\int \cot x dx=\ln|\sin x|+C$
    8. $\int \sec x dx=\ln|\sec x+\tan x|+C$
    9. $\int \csc x dx=-\ln|\csc x+\cot x|+C$
4. 定积分的计算方法：
    1. 几何意义法：利用几何形状计算面积或体积；
    2. 分割求和法：将区间分成若干个小份，对每份进行近似计算求得和，然后取极限得到定积分；
    3. 牛顿 - 莱布尼茨公式：如果函数 $f(x)$ 在区间 $[a,b]$ 上连续，则 $\int_a^b f(x)dx=F(b)-F(a)$，其中 $F(x)$ 是 $f(x)$
       的一个原函数。