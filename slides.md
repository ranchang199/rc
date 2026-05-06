---
theme: unicorn
title: 迭代法
info: |
  算法设计与分析 第4章 基本的算法策略：4.1 迭代算法
class: text-center
transition: slide-left
drawings:
  persist: false
mdc: true
---
<style global>
.alg-note-card {
  box-sizing: border-box;
  width: 100%;
  border: 2px solid #111;
  padding: 0.2rem 0.28rem;
  background: #fff;
  font-size: 0.54rem;
  line-height: 1.42;
}

.alg-note-card .alg-note-title {
  font-size: 0.58rem;
  font-weight: 700;
}

.alg-note-card .alg-note-formula {
  margin-top: 0.08rem;
  font-size: 0.56rem;
  font-family: "Times New Roman", serif;
}

.alg-note-card .spacer {
  height: 0.28rem;
}

.two-cols-header.alg-shot,
.two-cols-header.alg-note-shot {
  grid-template-columns: minmax(0, 0.9fr) minmax(0, 1.1fr);
  column-gap: 0.72rem;
}

.two-cols-header.alg-note-shot {
  grid-template-columns: minmax(0, 1fr) minmax(0, 0.82fr);
}

.two-cols-header.alg-code-page {
  grid-template-columns: 1fr;
}

.two-cols-header.alg-code-page .col-right,
.two-cols-header.alg-code-page .col-bottom {
  display: none;
}

.two-cols-header.alg-code-page .col-left {
  grid-area: 2 / 1 / 3 / 3;
  padding: 0.24rem 0.4rem 0.58rem 0.4rem;
}

.two-cols-header .col-header {
  box-sizing: border-box;
  padding-top: 3.08rem;
}

.two-cols-header .alg-title {
  margin: 0;
  text-align: center;
  font-size: 1.7rem;
  font-weight: 700;
  line-height: 1.12;
  color: #000;
}

.two-cols-header.alg-shot .col-left,
.two-cols-header.alg-note-shot .col-left {
  padding: 0.24rem 0.05rem 0.58rem 0.16rem;
}

.two-cols-header.alg-shot .col-right,
.two-cols-header.alg-note-shot .col-right {
  padding: 0.24rem 0.05rem 0.58rem 0;
}

.two-cols-header.alg-shot .col-right {
  display: flex;
  align-items: center;
  justify-content: center;
}

.two-cols-header.alg-note-shot .col-right {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  gap: 0.28rem;
}

.two-cols-header .alg-side-text {
  font-size: 0.8rem;
  line-height: 1.42;
  color: #000;
}

.two-cols-header .alg-side-text p {
  margin: 0 0 0.14rem 0;
}

.two-cols-header .alg-side-text ul {
  margin: 0.08rem 0 0.16rem 1.05rem;
  padding: 0;
}

.two-cols-header .alg-side-text li {
  margin: 0.04rem 0;
}

.two-cols-header .alg-side-text table {
  width: 100%;
  margin: 0.14rem 0;
  border-collapse: collapse;
  font-size: 0.6rem;
  line-height: 1.22;
}

.two-cols-header .alg-side-text th,
.two-cols-header .alg-side-text td {
  border: 1px solid #777;
  padding: 0.05rem 0.08rem;
  text-align: center;
  vertical-align: middle;
}

.two-cols-header.alg-shot .katex-display,
.two-cols-header.alg-note-shot .katex-display {
  margin: 0.12rem 0 0.18rem 0;
  font-size: 0.84em;
}

.two-cols-header.alg-shot pre.slidev-code,
.two-cols-header.alg-note-shot pre.slidev-code,
.two-cols-header.alg-code-page pre.slidev-code {
  margin: 0.2rem 0 0 0 !important;
  padding: 0.18rem 0.22rem !important;
  border: 2px solid #111;
  border-radius: 0;
  background: #f6f6f6 !important;
  box-shadow: none !important;
}

.two-cols-header.alg-shot pre.slidev-code code,
.two-cols-header.alg-note-shot pre.slidev-code code,
.two-cols-header.alg-code-page pre.slidev-code code {
  background: transparent !important;
}

.two-cols-header.alg-shot pre.slidev-code,
.two-cols-header.alg-note-shot pre.slidev-code {
  font-size: 0.39rem;
  line-height: 1.06;
}

.two-cols-header.alg-code-page pre.slidev-code {
  max-width: 14.25rem;
  margin: 0.34rem auto 0 auto !important;
  font-size: 0.39rem;
  line-height: 1.06;
}

.two-cols-header.alg-shot.alg-shot-tight pre.slidev-code,
.two-cols-header.alg-note-shot.alg-shot-tight pre.slidev-code,
.two-cols-header.alg-code-page.alg-shot-tight pre.slidev-code {
  font-size: 0.37rem;
  line-height: 1.04;
}

.two-cols-header.alg-shot.alg-shot-compact pre.slidev-code,
.two-cols-header.alg-note-shot.alg-shot-compact pre.slidev-code,
.two-cols-header.alg-code-page.alg-shot-compact pre.slidev-code {
  font-size: 0.35rem;
  line-height: 1.02;
}

img.alg-shot-img {
  display: block;
  width: 100%;
  max-width: 12.8rem;
  height: auto;
  margin: 0 auto;
  padding: 0.14rem;
  border: 2px solid #111;
  background: #fff;
  box-sizing: border-box;
}

img.alg-shot-img.narrow {
  max-width: 5.35rem;
}

.two-cols-header.rabbit-slide .col-header {
  padding-top: 0 !important;
}

.two-cols-header.rabbit-slide .alg-title {
  font-size: 1.5rem;
  line-height: 1.08;
}

.two-cols-header.rabbit-slide .col-left {
  padding: 0.3rem 0.04rem 0.58rem 0.16rem;
  font-size: 0.56rem;
  line-height: 1.32;
}

.two-cols-header.rabbit-slide .col-left p {
  margin: 0 0 0.12rem 0;
}

.two-cols-header.rabbit-slide .col-left ul {
  margin: 0.06rem 0 0.16rem 0.95rem;
}

.two-cols-header.rabbit-slide .col-left li {
  margin: 0.02rem 0;
}

.two-cols-header.rabbit-slide .col-left table {
  width: 100%;
  margin: 0.08rem 0 0.12rem 0;
  border-collapse: collapse;
  font-size: 0.46rem;
  line-height: 1.16;
}

.two-cols-header.rabbit-slide .col-left th,
.two-cols-header.rabbit-slide .col-left td {
  border: 1px solid #777;
  padding: 0.04rem 0.06rem;
  text-align: center;
  vertical-align: middle;
}

.two-cols-header.rabbit-slide .col-left .katex-display {
  margin: 0.08rem 0 0.12rem 0;
  font-size: 0.72em;
}

.two-cols-header.rabbit-slide .col-left pre.slidev-code {
  margin-top: 0.14rem !important;
  font-size: 0.33rem;
  line-height: 1.04;
}

.two-cols-header.rabbit-slide .col-right {
  align-items: flex-start;
  padding: 0.4rem 0.02rem 0.58rem 0;
}

.two-cols-header.rabbit-slide img.alg-shot-img {
  max-width: 7.2rem;
}

.two-cols-header.rabbit-slide.rabbit-2 .col-left {
  font-size: 0.54rem;
}

.two-cols-header.rabbit-slide.rabbit-2 .col-left table {
  font-size: 0.43rem;
}

.two-cols-header.rabbit-slide.rabbit-2 .col-left pre.slidev-code {
  font-size: 0.31rem;
}

.two-cols-header.rabbit-slide.rabbit-3 .col-left pre.slidev-code {
  font-size: 0.34rem;
}
</style>

  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">1</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">算法设计与分析</h1>

## 第 4 章 基本的算法策略

<div class="mt-12 text-left inline-block text-xl leading-10">

- 4.1 迭代算法
- 4.2 蛮力法
- 4.3 分而治之算法
- 4.4 贪婪算法
- 4.5 动态规划
- 4.6 算法策略间的比较

</div>

<div style="height:0.35rem;"></div>

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">2</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">4.1 迭代算法</h1>

## 基本思想

用旧值计算新值，一般用于数值计算。

## 常见迭代策略

- 累加
- 累乘

## 基本步骤

1. 确定迭代模型
2. 建立迭代关系式
3. 对迭代过程进行控制

停止方式：

- 固定次数结束
- 满足特定条件结束

<div style="height:0.35rem;"></div>

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">3</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">4.1.1 递推法</h1>

## 例 1：兔子繁殖问题

一对兔子从出生后第三个月开始，每月生一对小兔子。小兔子到第三个月又开始生下一代小兔子。假若兔子只生不死，一月份抱来一对刚出生的小兔子，问一年中每个月各有多少只兔子。

| 月份 | 1月 | 2月 | 3月 | 4月 | 5月 |
|---|---:|---:|---:|---:|---:|
| 数量 | 1 | 1 | 1+1=2 | 2+1=3 | 3+2=5 |

## 数学模型

$$
y_1=y_2=1,\quad y_n=y_{n-1}+y_{n-2},\quad n=3,4,\ldots
$$

数据结构可使用数组存储 $y_n$，也可使用变量存储当前迭代值。

<div style="height:0.35rem;"></div>

---
layout: two-cols-header
layoutClass: alg-shot rabbit-slide rabbit-1
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">4</div>

<div style="height:3.08rem;"></div>
<h1 class="alg-title" style="margin:0;">兔子繁殖：算法 1</h1>

::left::

递推关系：

$$
y_n=y_{n-1}+y_{n-2}
$$

变量含义：

- `a`：前 2 个月的数量
- `b`：前 1 个月的数量
- `c`：当前的数量

循环不变式：

$$
c=a+b
$$

```c
{
  int i, a = 1, b = 1, c;
  print(a, b);
  for (i = 1; i <= 10; i++) {
    c = a + b;
    print(c);
    a = b;
    b = c;
  }
}
```

::right::

<img src="/ppt-image2.png" class="alg-shot-img" />

---
layout: two-cols-header
layoutClass: alg-shot rabbit-slide rabbit-2
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">5</div>

<div style="height:3.08rem;"></div>
<h1 class="alg-title" style="margin:0;">兔子繁殖：算法 2</h1>

::left::

一次循环递推 3 步。

递推迭代表达式：

| 位置 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| 变量 | a | b | c=a+b | a=b+c | b=a+c | c=a+b | a=b+c | b=a+c |

$$
c=a+b;\quad a=b+c;\quad b=a+c
$$

```c
{
  int i, a = 1, b = 1, c;
  print(a, b);

  for (i = 1; i <= 4; i++) {
    c = a + b;
    a = b + c;
    b = c + a;
    print(a, b, c);
  }
}
```

::right::

<img src="/ppt-image2.png" class="alg-shot-img" />

---
layout: two-cols-header
layoutClass: alg-shot rabbit-slide rabbit-3
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">6</div>

<div style="height:3.08rem;"></div>
<h1 class="alg-title" style="margin:0;">兔子繁殖：算法 3</h1>

::left::

递推迭代表达式：

| 位置 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| 变量 | a | b | a=a+b | b=a+b | a=a+b | b=a+b |

$$
a=a+b;\quad b=a+b
$$

```c
{
  int i, a = 1, b = 1;
  print(a, b);

  for (i = 1; i <= 5; i++) {
    a = a + b;
    b = a + b;
    print(a, b);
  }
}
```

::right::

<img src="/ppt-image2.png" class="alg-shot-img" />

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">7</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">4.1.1 递推法</h1>

<div style="max-width:14rem;margin:1.05rem auto 0 auto;text-align:left;">
  <div style="font-size:1.08rem;font-weight:700;line-height:1.45;margin-bottom:0.8rem;">例 2：求两个整数的最大公约数</div>
  <div style="font-size:1rem;line-height:1.7;margin-bottom:0.35rem;">算法设计思路：</div>
  <ol style="margin:0 0 0.9rem 1.4rem;padding:0;font-size:1rem;line-height:1.8;">
    <li>短除法</li>
    <li>辗转相除法，也称欧几里得算法</li>
  </ol>
  <div style="font-size:1.02rem;font-weight:700;line-height:1.45;">递推关系</div>
</div>

$$
\gcd(m,n)=\gcd(n,m\bmod n)
$$

<div style="height:0.35rem;"></div>

---
layout: two-cols-header
layoutClass: alg-note-shot
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">8</div>

<h1 class="alg-title" style="font-size:1.76rem;">最大公约数：辗转相除法</h1>

::left::

```c
{
  int a, b, c;
  input(a, b);

  if (b == 0) {
    print("data error");
    return;
  } else {
    c = a % b;
    while (c != 0) {
      a = b;
      b = c;
      c = a % b;
    }
  }

  print(b);
}
```

::right::

<div class="alg-note-card">
  <div class="alg-note-title">递推关系：</div>
  <div class="alg-note-formula">gcd(m,n)=gcd(n,m mod n)</div>
  <div class="spacer"></div>
  <div class="alg-note-title">循环不变式：</div>
  <div>c = a mod b</div>
  <div>a = b</div>
  <div>b = c</div>
</div>

<img src="/ppt-image3.png" class="alg-shot-img narrow" />

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">9</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">4.1.2 倒推法</h1>

<div style="max-width:13.5rem;margin:1.8rem auto 0 auto;text-align:left;">
  <div style="font-size:1.12rem;font-weight:700;line-height:1.45;margin-bottom:0.95rem;">正推与倒推</div>
  <ul style="margin:0 0 0 1.35rem;padding:0;font-size:1.08rem;line-height:1.9;">
    <li>迭代法：正推，由前向后求解问题</li>
    <li>倒推法：从后往前推解问题</li>
  </ul>
</div>

<div style="height:0.35rem;"></div>

---
layout: two-cols-header
layoutClass: alg-shot
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">10</div>

<h1 class="alg-title" style="font-size:1.64rem;">倒推法例 1：猴子吃桃问题</h1>

::left::

一只小猴子摘了若干桃子，每天吃现有桃的一半多一个，到第 10 天时就只有一个桃子了，求原有多少个桃？

递推数学模型：

$$
a_i=(1+a_{i+1})\times 2,\quad i=9,8,7,\ldots
$$

循环不变式：

$$
a=(1+a)\times 2
$$

```c
{
  int i, s;
  s = 1;

  for (i = 9; i >= 1; i = i - 1)
    s = (s + 1) * 2;

  print(s);
}
```

::right::

<img src="/ppt-image4.png" class="alg-shot-img" />

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">11</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">倒推法例 2：杨辉三角形</h1>

## 用一维数组输出

```text
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
```

算法设计思路：

1. 用一维数组 `A[1..i]` 存储第 `i` 行
2. 若只用一维数组，正推会覆盖上一行对应的值，不能求下一个值
3. 反推法可以避免覆盖

二维递推式：

$$
a[i][j]=a[i-1][j-1]+a[i-1][j]
$$

<div style="height:0.35rem;"></div>

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">12</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">杨辉三角形：正推与反推</h1>

<img src="/ppt-image5.png" class="ref-figure" style="position:absolute;right:0.55rem;bottom:1.72rem;width:11.15rem;height:auto;z-index:6;opacity:0.97;background:white;padding:0.28rem;border:1px solid #d7deea;border-radius:0.45rem;box-shadow:0 8px 22px rgba(20,40,80,0.13);" />


## 正推会覆盖旧值

```text
1
1   1
1   2   1
1   3   4   1
1   4   8   9   1
```

## 反推保持正确结果

```text
1
1   1
1   2   1
1   3   3   1
1   4   6   4   1
```

关键关系：

$$
A[1]=A[i]=1
$$

正推：

$$
A[j]=A[j-1]+A[j],\quad j=2,3,\ldots,i-1
$$

反推：

$$
A[j]=A[j-1]+A[j],\quad j=i-1,i-2,\ldots,2
$$

<div style="height:0.35rem;"></div>

---
layout: two-cols-header
layoutClass: alg-code-page alg-shot-tight
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">13</div>

<h1 class="alg-title">杨辉三角形：算法</h1>

::left::

```c
{
  int n, i, j, a[100];
  input(n);
  print("1");
  print("\n");
  a[1] = a[2] = 1;
  print(a[1], a[2]);
  print("\n");
  for (i = 3; i <= n; i = i + 1) {
    a[1] = a[i] = 1;
    for (j = i - 1; j > 1; j--)
      a[j] = a[j] + a[j - 1];
    for (j = 1; j <= i; j = j + 1)
      print(a[j]);
    print("\n");
  }
}
```

<div style="height:0.35rem;"></div>

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">14</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">倒推法例 3：穿越沙漠问题</h1>

用一辆吉普车穿越 1000 公里的沙漠。吉普车的总装油量为 500 加仑，耗油率为 1 加仑/公里。由于沙漠中没有油库，必须先用这辆车在沙漠中建立临时油库。该吉普车以最少的耗油量穿越沙漠，应在什么地方建油库，以及各处的贮油量。

## 最省油方案

从 `a` 点到 `b` 点：

- 每次从 `a` 点加满油出发
- `a-b` 之间来回奇数次，最后一次朝 `b` 点走
- `a` 点储油量 = `a-b` 之间耗油量 + `b` 点储油量

<div style="height:0.35rem;"></div>

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">15</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">穿越沙漠：数学模型</h1>

变量含义：

- `k`：从 `a` 加满油向 `b` 出发的次数
- `2k-1`：`a-b` 之间的来回次数
- `x`：`a-b` 之间距离
- `S1`：`a` 加油点的储油量
- `S2`：`b` 加油点的储油量

数学模型：

$$
S_1=500k
$$

$$
S_2=S_1-(2k-1)x=500k-(2k-1)x
$$

<div style="height:0.35rem;"></div>

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">16</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">穿越沙漠：倒推设计</h1>

1. 第一段：倒数第一个储油点到终点

$$
k=1,\quad S_2=0,\quad x=500,\quad S_1=500
$$

2. 第二段：倒数 2 到倒数 1 储油点

$$
S_1>500,\quad k=2,\quad S_1=1000
$$

$$
x=\frac{1000-500}{2\times2-1}=\frac{500}{3}
$$

3. 第三段：倒数 3 到倒数 2 储油点

$$
S_1>1000,\quad k=3,\quad S_1=1500
$$

$$
x=\frac{1500-1000}{3\times2-1}=\frac{500}{5}
$$

<div style="height:0.35rem;"></div>

---
layout: two-cols-header
layoutClass: alg-shot alg-shot-tight
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">17</div>

<h1 class="alg-title">穿越沙漠：算法</h1>

::left::

```c
{
  int dis, k, oil;

  dis = 500;
  k = 1;
  oil = 500;

  do {
    print(k, 1000 - dis, oil);
    k = k + 1;
    dis = dis + 500 / (2 * k - 1);
    oil = 500 * k;
  } while (dis < 1000);

  oil = 500 * (k - 1) + (1000 - dis) * (2 * k - 1);
  print(k, 0, oil);
}
```

::right::

<img src="/ppt-image6.png" class="alg-shot-img" />

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">18</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">4.1.3 迭代法解方程</h1>

<div style="max-width:14.5rem;margin:1.05rem auto 0 auto;text-align:left;">
  <div style="font-size:1.08rem;font-weight:700;line-height:1.45;margin-bottom:0.45rem;">基本思想</div>
  <div style="font-size:1rem;line-height:1.8;margin-bottom:0.8rem;">逐步逼近。</div>
  <div style="font-size:1.08rem;font-weight:700;line-height:1.45;margin-bottom:0.35rem;">基本步骤</div>
  <ol style="margin:0 0 0 1.4rem;padding:0;font-size:1rem;line-height:1.8;">
    <li>确定初值 $x_0$</li>
    <li>建立迭代关系</li>
  </ol>
</div>

$$
f(x)=0 \Rightarrow x=\varphi(x)
$$

<div style="max-width:14.5rem;margin:0 auto;text-align:left;">
  <ol start="3" style="margin:0 0 0 1.4rem;padding:0;font-size:1rem;line-height:1.8;">
    <li>构造数列</li>
  </ol>
</div>

$$
x_n=\varphi(x_{n-1})
$$

<div style="max-width:14.5rem;margin:0 auto;text-align:left;">
  <ol start="4" style="margin:0 0 0 1.4rem;padding:0;font-size:1rem;line-height:1.8;">
    <li>直到满足停止条件</li>
  </ol>
</div>

<div style="height:0.35rem;"></div>

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">19</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">解方程组根</h1>

<div style="max-width:14.8rem;margin:1.1rem auto 0 auto;text-align:left;">
  <div style="font-size:1.08rem;font-weight:700;line-height:1.45;margin-bottom:0.8rem;">例 1：迭代法求方程组根</div>
  <div style="font-size:1rem;line-height:1.75;margin-bottom:0.2rem;">方程组解的初值：</div>
</div>

$$
X=(x_0,x_1,\ldots,x_{n-1})
$$

<div style="max-width:14.8rem;margin:0.2rem auto 0 auto;text-align:left;">
  <div style="font-size:1rem;line-height:1.75;margin-bottom:0.2rem;">迭代关系方程组：</div>
</div>

$$
x_i=g_i(X),\quad i=0,1,\ldots,n-1
$$

<div style="max-width:14.8rem;margin:0.15rem auto 0 auto;text-align:left;font-size:1rem;line-height:1.75;">
  其中 <span style="font-family:'Times New Roman',serif;">w</span> 为解的精度。
</div>

<div style="height:0.35rem;"></div>

---
layout: two-cols-header
layoutClass: alg-code-page alg-shot-tight
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">20</div>

<h1 class="alg-title" style="font-size:1.72rem;">方程组迭代算法</h1>

::left::

```c
for (i = 0; i < n; i++)
  x[i] = 初始近似根;

do {
  k = k + 1;

  for (i = 0; i < n; i++)
    y[i] = x[i];

  for (i = 0; i < n; i++)
    x[i] = gi(X);

  for (i = 0; i < n; i++)
    c = c + fabs(y[i] - x[i]);

} while (c > w && k < maxn);

for (i = 0; i < n; i++)
  print(i, "变量的近似根是", x[i]);
```

<div style="height:0.35rem;"></div>

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">21</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">牛顿迭代法求根</h1>

<div style="max-width:14.5rem;margin:1.05rem auto 0 auto;text-align:left;">
  <div style="font-size:1.08rem;font-weight:700;line-height:1.45;margin-bottom:0.7rem;">例 2</div>
  <div style="font-size:1rem;line-height:1.75;margin-bottom:0.2rem;">用牛顿迭代法求形如</div>
</div>

$$
ax^3+bx^2+cx+d=0
$$

<div style="max-width:14.5rem;margin:0.15rem auto 0 auto;text-align:left;">
  <div style="font-size:1rem;line-height:1.75;margin-bottom:0.35rem;">方程的根。</div>
  <div style="font-size:1rem;line-height:1.75;margin-bottom:0.2rem;">由切线近似：</div>
</div>

$$
f(x_0)+f'(x_0)(x-x_0)\approx0
$$

<div style="max-width:14.5rem;margin:0.15rem auto 0 auto;text-align:left;">
  <div style="font-size:1rem;line-height:1.75;margin-bottom:0.2rem;">可得：</div>
</div>

$$
x=x_0-\frac{f(x_0)}{f'(x_0)}
$$

<div style="height:0.35rem;"></div>

---
layout: two-cols-header
layoutClass: alg-shot alg-shot-tight
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">22</div>

<h1 class="alg-title">牛顿迭代法：算法</h1>

::left::

示例方程：

$$
x^3+2x^2+3x+4=0
$$

```c
{
  float a, b, c, d, fx;
  print("输入系数 a,b,c,d:");
  input(a, b, c, d);

  fx = f(a, b, c, d);
  printf("方程的根为：", fx);
}

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

::right::

<img src="/ppt-image7.png" class="alg-shot-img" />

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">23</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">二分法求方程根</h1>

<div style="max-width:14.5rem;margin:1.05rem auto 0 auto;text-align:left;">
  <div style="font-size:1.08rem;font-weight:700;line-height:1.45;margin-bottom:0.7rem;">例 3</div>
  <div style="font-size:1rem;line-height:1.75;margin-bottom:0.2rem;">二分法求解方程</div>
</div>

$$
\frac{x^3}{2}+2x^2-8=0
$$

<div style="max-width:14.5rem;margin:0.15rem auto 0 auto;text-align:left;">
  <div style="font-size:1rem;line-height:1.75;margin-bottom:0.6rem;">在区间 <span style="font-family:'Times New Roman',serif;">[0, 1]</span> 上的近似根。</div>
  <div style="font-size:1.08rem;font-weight:700;line-height:1.45;margin-bottom:0.25rem;">前提条件</div>
  <div style="font-size:1rem;line-height:1.75;margin-bottom:0.2rem;"><span style="font-family:'Times New Roman',serif;">f(x)</span> 在求解区间 <span style="font-family:'Times New Roman',serif;">[a,b]</span> 上连续，且 <span style="font-family:'Times New Roman',serif;">f(a)</span> 与 <span style="font-family:'Times New Roman',serif;">f(b)</span> 异号：</div>
</div>

$$
f(a)\times f(b)<0
$$

<div style="height:0.35rem;"></div>

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">24</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">二分法：算法设计</h1>

1. 取初始区间

$$
[a_0,b_0]=[a,b],\quad c_0=\frac{a_0+b_0}{2}
$$

2. 判断中点

- 若 $f(c_0)=0$，则 $c_0$ 为根
- 若 $f(a_0)f(c_0)<0$，则 $[a_1,b_1]=[a_0,c_0]$
- 若 $f(b_0)f(c_0)<0$，则 $[a_1,b_1]=[c_0,b_0]$

3. 终止条件

当 $f(c_n)=0$，或区间 $[a_n,b_n]$ 足够小，就认为找到了方程的根。

<div style="height:0.35rem;"></div>

---
layout: two-cols-header
layoutClass: alg-shot alg-shot-compact
class: text-left
---

<img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
<div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
<div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
<div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
<div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">25</div>

<h1 class="alg-title">二分法：算法</h1>

::left::

```c
{
  float x, x1 = 0, x2 = 2, f1, f2, f;
  input(a, b);
  f1 = x1 * x1 * x1 / 2 + 2 * x1 * x1 - 8;
  f2 = x2 * x2 * x2 / 2 + 2 * x2 * x2 - 8;
  if (f1 * f2 > 0) {
    printf("No root");
    return;
  }
  do {
    x = (x1 + x2) / 2;
    f = x * x * x / 2 + 2 * x * x - 8;
    if (f == 0)
      break;
    if (f1 * f > 0.0) {
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

::right::

<img src="/ppt-image8.png" class="alg-shot-img" />

---


  <img src="/wust-logo.png" style="position:absolute;left:0.2rem;top:0.08rem;width:9.5rem;height:auto;z-index:10;" />
  <div style="position:absolute;left:0;right:0;top:2.72rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:0;right:0;bottom:1.2rem;border-top:1.5px solid #2c57ff;z-index:9;"></div>
  <div style="position:absolute;left:1.1rem;bottom:0.22rem;color:#e00000;font-size:0.72rem;line-height:1;font-family:'Times New Roman','SimSun',serif;z-index:10;">5/5/2026 4:50 PM</div>
  <div style="position:absolute;left:50%;bottom:0.2rem;transform:translateX(-50%);color:#e00000;font-size:0.78rem;line-height:1;font-family:'STXingkai','KaiTi',serif;z-index:10;">算法设计与分析</div>
  <div style="position:absolute;right:1rem;bottom:0.22rem;color:#e00000;font-size:0.82rem;line-height:1;font-style:italic;font-family:'Times New Roman',serif;z-index:10;">26</div>
<div style="height:3.12rem;"></div>
<h1 style="margin:0 0 0.95rem 0;text-align:center;font-size:1.88rem;font-weight:700;line-height:1.2;color:#000000;">小结</h1>

## 本节核心

- 迭代算法通过“旧值求新值”不断逼近或构造结果
- 递推法适合从已知初始项逐步推出后续项
- 倒推法适合由终止状态反向恢复初始状态
- 解方程时常用固定点迭代、牛顿迭代和二分法

## 关键问题

- 如何建立迭代关系式
- 如何选择初值
- 如何设置停止条件
- 如何避免覆盖仍需使用的旧数据

<div style="height:0.35rem;"></div>











