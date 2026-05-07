---
theme: default
title: 迭代法
colorSchema: light
info: |
  基于《算法设计与分析》第 4 章 4.1 迭代算法内容，使用 Slidev + Markdown 代码化制作。
class: text-center
drawings:
  persist: false
transition: slide-left
css: ./style.css
---

# 迭代算法

算法设计与分析  
第 4 章：基本的算法策略

<div class="kicker">Iteration Method</div>

<div class="scribble-box">
从“重复计算”到“逐步逼近”：理解算法中最基础、最常见的一类思维方式。
</div>

---
layout: default
---

# 为什么要学迭代？

很多问题不能“一步算出答案”，但可以通过不断更新状态逐步接近目标。

典型场景：

- 数列问题：由前几项推出后几项
- 状态问题：每一步都由上一步决定
- 数值问题：无法直接求精确解，只能逐步逼近
- 程序实现：循环结构天然适合表达迭代过程

<div class="mark-box">
迭代思想的本质：把复杂问题拆成一系列<span class="red">重复的小步骤</span>。
</div>

---
layout: default
---

# 本节学习目标

学完本节后，你应该能回答 4 个问题：

1. 什么是<span class="circle-red-sm">迭代算法</span>？
2. 递推法和倒推法有什么区别？
3. 如何根据问题建立<span class="red">迭代关系式</span>？
4. 如何用迭代思想求方程的近似根？

<div class="note">
一句话理解：迭代就是从一个已知状态出发，按照固定规则不断更新状态，直到得到目标结果。
</div>

---
layout: default
---

# 本课聚焦：4.1 迭代算法

本章内容包括：

- 4.1 <span class="red">迭代算法</span> ← 本课重点
- 4.2 蛮力法
- 4.3 分而治之算法
- 4.4 贪婪算法
- 4.5 动态规划
- 4.6 算法策略间的比较

<div class="note">
本节主要讨论三类迭代思想：递推法、倒推法、迭代求根。
</div>

---
layout: default
---

# 4.1 迭代算法

基本思想：<span class="circle-red">用旧值计算新值</span>。

迭代算法常用于：

- 数列递推
- 状态更新
- 数值计算
- 方程近似求根

基本步骤：

1. 确定初始状态
2. 建立<span class="red">迭代关系式</span>
3. 重复更新状态
4. 根据<span class="red">停止条件</span>结束循环

<div class="process-grid">
  <div class="process-card"><strong>输入</strong><br>初值、边界、精度</div>
  <div class="process-card"><strong>规则</strong><br>由旧值推出新值</div>
  <div class="process-card"><strong>更新</strong><br>循环推进当前状态</div>
  <div class="process-card"><strong>终止</strong><br>次数上限或误差足够小</div>
</div>

---
layout: default
class: text-center
---

# 迭代算法总流程

<div class="flow-mini">

<span class="step">确定初始状态</span>
<span class="arrow">↓</span>
<span class="step">建立迭代关系式</span>
<span class="arrow">↓</span>
<span class="step">根据旧值计算新值</span>
<span class="arrow">↓</span>
<span class="step"><span class="circle-red-sm">判断停止条件</span></span>
<span class="arrow">↓</span>
<span class="step">输出结果</span>

</div>

<div class="scribble-box">
迭代算法的核心不是某一个公式，而是<span class="red">状态不断更新</span>的过程。
<div class="formula-note">考试、作业、编程实现时，这一句往往就是“本质”。</div>
</div>

---
layout: default
class: text-center
---

# 迭代算法的三种典型形式

| 类型 | 核心思想 | 常见问题 |
|---|---|---|
| <span class="red">递推法</span> | 已知前面，推出后面 | 兔子繁殖、最大公约数 |
| <span class="red">倒推法</span> | 已知结果，反推开始 | 猴子吃桃、穿越沙漠 |
| <span class="red">迭代求根</span> | 从猜测值出发，逐步逼近 | 牛顿法、二分法 |

<div class="note">
本课主线：先理解“状态如何更新”，再看不同问题中更新方向有什么变化。
</div>

---
layout: default
class: text-center
---

# 递推法

<div class="kicker">Forward Recurrence</div>

递推法：<span class="circle-red">从已知状态出发</span>，一步步推出后续状态。

常见特点：

- 已知初始条件
- 能写出相邻状态之间的关系
- 通过循环不断向后计算

<div class="scribble-box">
大白话：知道前面怎么算后面。
</div>

---
layout: default
---

# 4.1.1 递推法：兔子繁殖问题

一对兔子从出生后第三个月开始，每月生一对小兔子。小兔子到第三个月又开始生下一代小兔子。若兔子只生不死，一月份抱来一对刚出生的小兔子，问一年中每个月各有多少<span class="red">对</span>兔子。

<table class="matrix">
  <thead>
    <tr><th>月份</th><th>1月</th><th>2月</th><th>3月</th><th>4月</th><th>5月</th></tr>
  </thead>
  <tbody>
    <tr><td>兔子对数</td><td>1</td><td>1</td><td>2</td><td>3</td><td>5</td></tr>
  </tbody>
</table>

数学模型：

$$
y_1 = y_2 = 1,\quad y_n = y_{n-1} + y_{n-2},\quad n \ge 3
$$

<div class="formula-note">
<span class="hand-note">注意</span>：这里是“兔子对数”，不是“兔子只数”。
</div>

---
layout: two-cols
---

# 递推算法 1：每轮生成 1 个新值

递推关系：

$$
y_n = y_{n-1} + y_{n-2}
$$

<div class="mark-box">

变量含义：

- `a`：前 2 个月的兔子对数
- `b`：前 1 个月的兔子对数
- `c`：当前月份的兔子对数

</div>

<div class="terminal-flow">状态更新
c = a + b
a = b
b = c</div>

<div class="code-tip">
这是最适合考试书写和课堂讲解的版本，因为每轮只推进一步，变量含义最清楚。
</div>

::right::

```c {all|3|6-8}
main()
{
  int i, a = 1, b = 1, c;
  print(a, b);

  for (i = 3; i <= 12; i++) {
    c = a + b;
    print(c);
    a = b;
    b = c;
  }
}
```

<div class="formula-note">
<span class="arrow-note">关键</span>：每轮只生成一个新值，最直观。
</div>

---
layout: two-cols
---

# 递推算法 2：每轮生成 3 个新值

一次循环连续递推 <span class="circle-red">3 步</span>。

<div class="mark-box">

变量更新关系：

```text
c = a + b
a = b + c
b = c + a
```

</div>

如果要按自然顺序输出，应输出：

```text
c, a, b
```

::right::

```c {all|6-8}
main()
{
  int i, a = 1, b = 1, c;
  print(a, b);

  for (i = 1; i <= 4; i++) {
    c = a + b; print(c);
    a = b + c; print(a);
    b = c + a; print(b);
  }
}
```

<div class="formula-note">
<span class="hand-note">注意</span>：更新顺序不能乱，初学时优先掌握算法 1。
</div>

---
layout: two-cols
---

# 递推算法 3：每轮生成 2 个新值

该写法每轮循环产生 <span class="circle-red-sm">2 个新值</span>。

变量更新关系：

```text
a = a + b
b = a + b
```

输出顺序就是：

```text
a, b
```

<div class="note small">
三种写法本质相同，都是用前两项推出后一项。
</div>

::right::

```c {all|6|9}
main()
{
  int i, a = 1, b = 1;
  print(a, b);

  for (i = 1; i <= 5; i++) {
    a = a + b;
    print(a);

    b = a + b;
    print(b);
  }
}
```

<div class="formula-note">
<span class="arrow-note">核心</span>：变量保存的是“当前递推状态”。
</div>

---
layout: default
---

# 递推法：最大公约数

例：求两个整数的最大公约数。

常见方法：

1. 短除法
2. <span class="red">辗转相除法</span>，也称欧几里得算法

核心递推关系：

$$
\gcd(a,b)=\gcd(b,a\bmod b)
$$

终止条件：

$$
b=0
$$

此时：

$$
\gcd(a,b)=a
$$

<div class="scribble-box">
关键理解：每次把问题变小，但最大公约数不变。
</div>

---
layout: two-cols
---

# 欧几里得算法

<div class="terminal-flow">变量更新
c = a mod b
a = b
b = c</div>

算法思想：

- 每次用余数替换较小问题
- 最大公约数不变
- 余数最终变为 <span class="circle-red-sm">0</span>

<div class="code-tip">
和“枚举所有公因数”相比，它不是在试答案，而是在持续缩小问题规模。
</div>

::right::

```c {all|6-7|9-13}
main()
{
  int a, b, c;
  input(a, b);

  if (a == 0 && b == 0) {
    print("data error");
    return;
  }

  a = abs(a);
  b = abs(b);

  while (b != 0) {
    c = a % b;
    a = b;
    b = c;
  }

  print(a);
}
```

<div class="formula-note">
<span class="arrow-note">比枚举更强</span>：不断缩小问题规模。
</div>

---
layout: default
class: text-center
---

# 递推法与倒推法对比

<div class="compare-grid">
  <div class="compare-card">
    <h3>递推法</h3>
    <p>从前往后，根据已知初始状态不断更新。</p>
    <p class="muted">典型：兔子繁殖、最大公约数</p>
  </div>
  <div class="compare-card">
    <h3>倒推法</h3>
    <p>从后往前，根据最终状态反向恢复。</p>
    <p class="muted">典型：猴子吃桃、穿越沙漠</p>
  </div>
</div>

<div class="mark-box">
判断方法：如果题目给的是“起点”，通常用递推；如果题目给的是“最终结果”，通常考虑倒推。
</div>

---
layout: default
class: text-center
---

# 4.1.2 倒推法

<div class="kicker">Backward Iteration</div>

倒推法：<span class="circle-red">从结果出发</span>，反向恢复初始状态。

常见特点：

- 最终状态已知
- 正向推导不方便
- 反向关系更容易建立

<div class="scribble-box">
大白话：知道最后变成什么样，再倒着算最开始是什么样。
</div>

---
layout: two-cols
---

# 倒推法：猴子吃桃

一只小猴子摘了若干桃子，每天吃现有桃的一半多一个。到第 10 天时只剩 1 个桃子，求原有多少个桃？

正向关系：

```text
第二天桃子数 = 第一天桃子数 / 2 - 1
```

倒推关系：

$$
a_i=(a_{i+1}+1)\times 2,\quad i=9,8,7,\ldots,1
$$

<div class="formula-note">
<span class="arrow-note">关键</span>：从第 10 天的 1 个桃子开始反推。
</div>

::right::

```c {all|4-6}
main()
{
  int i, s;
  s = 1;

  for (i = 9; i >= 1; i--) {
    s = (s + 1) * 2;
  }

  print(s);
}
```

<div class="terminal-flow">倒推链条
第 10 天：1
第 9 天：(1 + 1) × 2
第 8 天：继续倒推
...
第 1 天：得到原始桃子数</div>

---
layout: two-cols
---

# 倒推法：杨辉三角

例：用一维数组输出杨辉三角形。

```text
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
```

二维递推关系：

$$
a[i][j]=a[i-1][j-1]+a[i-1][j]
$$

<div class="mark-box">
如果用一维数组，需要避免<span class="red">新值覆盖旧值</span>。
</div>

::right::

正向更新会覆盖数据：

```text
A[j] = A[j-1] + A[j]
j = 2,3,...,i-1
```

倒向更新可以避免覆盖：

```text
A[j] = A[j-1] + A[j]
j = i-1,i-2,...,2
```

<div class="formula-note">
<span class="hand-note">重点</span>：从右向左更新。
</div>

---
layout: two-cols
---

# 杨辉三角代码

正向错误更新可能产生：

```text
1
1 1
1 2 1
1 3 4 1
1 4 8 9 1
```

倒向更新可以得到：

```text
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
```

<div class="formula-note">
<span class="arrow-note">原因</span>：倒向更新能保留上一行旧值。
</div>

::right::

```c {all|9-11}
main()
{
  int n, i, j, a[100];
  input(n);

  a[1] = 1;
  print(a[1]);

  for (i = 2; i <= n; i++) {
    a[i] = 1;

    for (j = i - 1; j >= 2; j--) {
      a[j] = a[j] + a[j - 1];
    }

    for (j = 1; j <= i; j++) {
      print(a[j]);
    }
  }
}
```

---
layout: default
---

# 为什么沙漠问题适合倒推？

穿越沙漠问题中，起点到底要准备多少油并不直观。

但终点附近很清楚：

- 最后一段最多只需要 <span class="red">500 加仑</span>油
- 最后一段最多能走 <span class="red">500 公里</span>
- 可以从终点向前反推出每一个储油点

<div class="scribble-box">
所以这个问题从终点开始倒推，比从起点正推更容易建立模型。
</div>

---
layout: two-cols
---

# 倒推法：穿越沙漠

用一辆吉普车穿越 1000 公里的沙漠。吉普车总装油量为 500 加仑，耗油率为 1 加仑/公里。沙漠中没有油库，必须先建立临时油库。

最省油方案：

- 每次从 `a` 点加满油出发
- `a-b` 之间来回奇数次，最后一次朝 `b` 点走
- `a` 点储油量 = `a-b` 之间耗油量 + `b` 点储油量

::right::

<div class="eq-box">
变量说明：

- `k`：从 `a` 加满油向 `b` 出发的次数
- `2k-1`：`a-b` 之间的行驶次数
- `x`：`a-b` 之间距离
- `S1`：`a` 点储油量
- `S2`：`b` 点储油量
</div>

数学模型：

$$
S_2 = 500k - (2k-1)x
$$

---
layout: two-cols
---

# 沙漠问题：倒推设计

第一段：倒数第一个储油点到终点

$$
k=1,\quad S_2=0,\quad x=500,\quad S_1=500
$$

第二段：倒数第二个储油点到倒数第一个储油点

$$
k=2,\quad S_1=1000,\quad x=\frac{1000-500}{2\times2-1}=\frac{500}{3}
$$

第三段：倒数第三个储油点到倒数第二个储油点

$$
k=3,\quad S_1=1500,\quad x=\frac{1500-1000}{2\times3-1}=\frac{500}{5}
$$

::right::

<div class="terminal-flow">空间关系
起点 ---- 储油点 a ---- 储油点 b ---- 终点
          S1 = 500k       S2
          距离 x
          行驶 2k - 1 次</div>

<div class="formula-note">
<span class="hand-note">圈重点</span>：倒推时先看离终点最近的一段。
</div>

---
layout: two-cols
---

# 沙漠问题代码

程序输出：

- 储油点序号
- 储油点距离
- 储油量

<div class="mark-box">
注意：该问题涉及非整数距离，应使用 <span class="red">double</span> 类型。
</div>

::right::

```c {all|4-6|8-11|13}
main()
{
  double dis, oil;
  int k;

  dis = 500.0;
  k = 1;
  oil = 500.0;

  do {
    print(k, 1000 - dis, oil);
    k = k + 1;
    dis = dis + 500.0 / (2 * k - 1);
    oil = 500.0 * k;
  } while (dis < 1000);

  oil = 500.0 * (k - 1) + (1000 - dis) * (2 * k - 1);
  print(k, 0, oil);
}
```

---
layout: default
class: text-center
---

# 4.1.3 迭代法解方程

<div class="kicker">Numerical Iteration</div>

迭代求根：<span class="circle-red">从一个猜测值出发</span>，不断逼近真实解。

常见方法：

- 牛顿迭代法
- 二分法

<div class="scribble-box">
大白话：先猜一个答案，再用规则不断修正它。
</div>

---
layout: default
---

# 迭代法解方程：基本框架

很多方程难以直接求出精确解，可以通过迭代获得近似解。

基本步骤：

1. 确定初值 $x_0$
2. 建立迭代关系：由 $f(x)=0$ 转换为 $x=\varphi(x)$
3. 构造数列：$x_n=\varphi(x_{n-1})$
4. 当误差小于精度要求时停止

<div class="terminal-flow">求根流程
选择初始值 x0
  ↓
计算新值 x1
  ↓
判断误差是否足够小
  ↓
若不满足：令 x0 = x1，继续迭代
若满足：输出近似根</div>

<div class="formula-note">
<span class="arrow-note">关键</span>：初值、迭代关系、停止条件缺一不可。
</div>

---
layout: default
---

# 迭代法求方程组根

已知方程组解的初值：

$$
X=(x_0,x_1,\ldots,x_{n-1})
$$

迭代关系方程组：

$$
x_i=g_i(X),\quad i=0,1,\ldots,n-1
$$

其中 `w` 为解的精度。

```c {all|4|7|10|13}
for (i = 0; i < n; i++)
  x[i] = 初始近似根;

do {
  c = 0;
  k = k + 1;

  for (i = 0; i < n; i++)
    y[i] = x[i];

  for (i = 0; i < n; i++)
    x[i] = g_i(y);

  for (i = 0; i < n; i++)
    c = c + fabs(y[i] - x[i]);

} while (c > w && k < maxn);
```

<div class="formula-note">
<span class="hand-note">注意</span>：每轮迭代前误差累计量 `c` 要清零。
</div>

---
layout: two-cols
---

# 牛顿迭代法求根

目标：求形如

$$
ax^3+bx^2+cx+d=0
$$

的方程根。

牛顿迭代思想：用切线近似曲线。

$$
f(x_0)+f'(x_0)(x-x_0)\approx 0
$$

因此：

$$
x_1=x_0-\frac{f(x_0)}{f'(x_0)}
$$

::right::

<div class="terminal-flow">牛顿更新
初值 x0
  ↓
计算 f(x0) 与 f'(x0)
  ↓
x1 = x0 - f(x0) / f'(x0)
  ↓
判断 |x1 - x0| 是否小于精度</div>

<div class="formula-note">
<span class="arrow-note">本质</span>：用切线交点更新下一次近似值。
</div>

---
layout: two-cols
---

# 牛顿迭代代码

示例：

$$
x^3+2x^2+3x+4=0
$$

停止条件：

$$
|x_1-x_0|<10^{-4}
$$

::right::

```c {all|5-9}
float f(float a, float b, float c, float d)
{
  float x1 = 1, x0, f0, f1;

  do {
    x0 = x1;
    f0 = ((a * x0 + b) * x0 + c) * x0 + d;
    f1 = (3 * a * x0 + 2 * b) * x0 + c;
    x1 = x0 - f0 / f1;
  } while (fabs(x1 - x0) >= 1e-4);

  return x1;
}
```

<div class="formula-note">
<span class="circle-red-sm">快</span>：牛顿法收敛快，但需要求导，而且对初值较敏感。
</div>

---
layout: two-cols
---

# 二分法求方程根

求解方程：

$$
f(x)=\frac{x^3}{2}+2x^2-8=0
$$

选取区间：

$$
[0,2]
$$

因为：

$$
f(0)=-8<0,\quad f(2)=4>0
$$

所以：

$$
f(0)f(2)<0
$$

满足二分法条件。

::right::

二分法前提：

- $f(x)$ 在区间 $[a,b]$ 上连续
- $f(a)$ 与 $f(b)$ <span class="red">异号</span>

基本思想：

<div class="terminal-flow">每次取中点 c = (a + b) / 2
保留仍然存在根的一半区间</div>

<div class="formula-note">
<span class="hand-note">重点</span>：二分法必须先保证区间两端异号。
</div>

---
layout: two-cols
---

# 二分法代码

停止条件：函数值足够接近 0。

$$
|f(x)|<10^{-4}
$$

<div class="mark-box">
二分法特点：<span class="red">稳定可靠</span>，但收敛速度比牛顿法慢。
</div>

::right::

```c {all|4-5|7-10|12-20}
main()
{
  float x, x1 = 0, x2 = 2, f1, f2, f;

  f1 = x1*x1*x1/2 + 2*x1*x1 - 8;
  f2 = x2*x2*x2/2 + 2*x2*x2 - 8;

  if (f1 * f2 > 0) {
    print("No root in this interval");
    return;
  }

  do {
    x = (x1 + x2) / 2;
    f = x*x*x/2 + 2*x*x - 8;

    if (f == 0) break;
    if (f1 * f > 0) {
      x1 = x;
      f1 = f;
    } else {
      x2 = x;
      f2 = f;
    }
  } while (fabs(f) >= 1e-4);

  print("root=", x);
}
```

---
layout: default
class: text-center
---

# 牛顿法 vs 二分法

| 方法 | 优点 | 缺点 | 适用情况 |
|---|---|---|---|
| <span class="red">牛顿法</span> | 收敛速度快 | 需要求导，对初值敏感 | 函数可导，初值较好 |
| <span class="red">二分法</span> | 稳定可靠 | 收敛速度较慢 | 已知根所在区间 |

<div class="scribble-box">
选择建议：能求导且初值较好，用牛顿法；只知道根所在区间，用二分法。
</div>

---
layout: default
class: text-center
---

# 小结

迭代算法的关键是：

<span class="circle-red">初值</span>、<span class="circle-red">关系式</span>、<span class="circle-red">更新过程</span>、<span class="circle-red">停止条件</span>。

<div class="compare-grid">
  <div class="compare-card">
    <h3>递推法</h3>
    <p>知道前面，推出后面。</p>
  </div>
  <div class="compare-card">
    <h3>倒推法</h3>
    <p>知道结果，反推开始。</p>
  </div>
  <div class="compare-card">
    <h3>迭代求根</h3>
    <p>从猜测值出发，逐步逼近真实解。</p>
  </div>
  <div class="compare-card">
    <h3>统一本质</h3>
    <p>复杂问题被拆成一次又一次状态更新。</p>
  </div>
</div>

<div class="mark-box">
迭代算法的本质不是公式堆砌，而是把复杂问题拆成一次又一次的<span class="red">状态更新</span>。
</div>

<div class="kicker">End</div>
