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
---

<div
  style="
    max-width: 980px;
    margin: 1.2rem auto 0;
    padding: 1.3rem 1.5rem 1.4rem;
    border-radius: 30px;
    background:
      radial-gradient(circle at 12% 18%, rgba(15, 118, 110, 0.16), transparent 22%),
      radial-gradient(circle at 86% 14%, rgba(201, 122, 20, 0.16), transparent 18%),
      linear-gradient(180deg, rgba(255,255,255,0.98), rgba(240,247,245,0.98));
    border: 1px solid rgba(17, 58, 82, 0.10);
    box-shadow: 0 24px 70px rgba(11, 36, 52, 0.12);
  "
>
  <div
    style="
      display: inline-block;
      padding: 0.22rem 0.72rem;
      border-radius: 999px;
      background: rgba(15, 118, 110, 0.10);
      border: 1px solid rgba(15, 118, 110, 0.18);
      color: #0f766e;
      font-size: 0.82rem;
      font-weight: 800;
      letter-spacing: 0.16em;
      text-transform: uppercase;
    "
  >
    Iteration Method
  </div>

  <h1
    style="
      margin: 0.55rem 0 0.2rem;
      font-size: 2.4rem;
      line-height: 1.04;
      font-weight: 900;
      color: #113a52;
    "
  >
    迭代算法
  </h1>

  <div
    style="
      color: #53657b;
      font-size: 1rem;
      letter-spacing: 0.04em;
      margin-bottom: 0.45rem;
    "
  >
    Algorithm Design · Chapter 4.1
  </div>

  <div
    style="
      font-size: 1.42rem;
      font-weight: 820;
      color: #1d3652;
      margin-bottom: 0.85rem;
    "
  >
    从重复计算到逐步逼近
  </div>

  <div
    style="
      padding: 0.95rem 1.05rem;
      border-radius: 22px;
      background: rgba(255,255,255,0.78);
      border: 1px dashed rgba(15, 118, 110, 0.26);
      color: #203247;
      line-height: 1.7;
      box-shadow: 0 12px 28px rgba(11, 36, 52, 0.08);
    "
  >
    这不是一份只背定义的课件，而是一张“算法状态如何更新”的工作台。
  </div>

  <div
    style="
      margin-top: 0.9rem;
      padding: 0.9rem 1rem;
      border-radius: 20px;
      background: linear-gradient(135deg, rgba(255, 241, 241, 0.98), rgba(255, 255, 255, 0.92));
      border: 1px solid rgba(214, 69, 69, 0.22);
      color: #16273b;
      box-shadow: 0 10px 24px rgba(214, 69, 69, 0.08);
    "
  >
    主线关键词：
    <span style="color:#d64545;font-weight:900;">初值</span>
    →
    <span style="color:#d64545;font-weight:900;">关系式</span>
    →
    <span style="color:#d64545;font-weight:900;">更新</span>
    →
    <span style="color:#d64545;font-weight:900;">停止条件</span>
  </div>

  <div
    style="
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 0.75rem;
      margin-top: 1rem;
    "
  >
    <div style="padding:0.75rem 0.6rem;border-radius:18px;background:rgba(255,255,255,0.84);box-shadow:0 10px 24px rgba(11,36,52,0.07);">
      <div style="font-size:1.35rem;font-weight:900;color:#0f766e;">Forward</div>
      <div style="color:#5f7086;font-size:0.84rem;">知道前面，推出后面</div>
    </div>
    <div style="padding:0.75rem 0.6rem;border-radius:18px;background:rgba(255,255,255,0.84);box-shadow:0 10px 24px rgba(11,36,52,0.07);">
      <div style="font-size:1.35rem;font-weight:900;color:#4856d6;">Backward</div>
      <div style="color:#5f7086;font-size:0.84rem;">知道结果，反推开始</div>
    </div>
    <div style="padding:0.75rem 0.6rem;border-radius:18px;background:rgba(255,255,255,0.84);box-shadow:0 10px 24px rgba(11,36,52,0.07);">
      <div style="font-size:1.35rem;font-weight:900;color:#c97a14;">Numerical</div>
      <div style="color:#5f7086;font-size:0.84rem;">猜测并不断逼近</div>
    </div>
  </div>
</div>

---
layout: default
---

# 为什么要学迭代？

<div
  style="
    max-width: 1040px;
    margin: 0.8rem auto 0;
    padding: 1rem 1.1rem 1.15rem;
    border-radius: 28px;
    background:
      radial-gradient(circle at 10% 14%, rgba(15,118,110,0.12), transparent 18%),
      linear-gradient(180deg, rgba(255,255,255,0.98), rgba(242,247,246,0.96));
    border: 1px solid rgba(17,58,82,0.10);
    box-shadow: 0 18px 50px rgba(11,36,52,0.10);
  "
>
  <p style="margin:0 0 0.85rem;color:#203247;line-height:1.7;">
    很多问题不能“一步算出答案”，但可以通过不断更新状态逐步接近目标。
  </p>

  <div
    style="
      display:grid;
      grid-template-columns: 1.25fr 1fr;
      gap: 0.9rem;
      align-items: stretch;
    "
  >
    <div
      style="
        padding: 0.95rem 1rem;
        border-radius: 22px;
        background: rgba(255,255,255,0.88);
        border: 1px solid rgba(17,58,82,0.08);
        box-shadow: 0 10px 24px rgba(11,36,52,0.06);
      "
    >
      <div style="font-size:0.95rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">典型场景</div>
      <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
        <div>1. 数列问题：由前几项推出后几项</div>
        <div>2. 状态问题：每一步都由上一步决定</div>
        <div>3. 数值问题：无法直接求精确解，只能逐步逼近</div>
        <div>4. 程序实现：循环结构天然适合表达迭代过程</div>
      </div>
    </div>

    <div
      style="
        padding: 0.95rem 1rem;
        border-radius: 22px;
        background: linear-gradient(180deg, rgba(255,255,255,0.96), rgba(240,244,255,0.86));
        border: 1px solid rgba(72,86,214,0.12);
        box-shadow: 0 10px 24px rgba(11,36,52,0.06);
      "
    >
      <div style="font-size:0.95rem;font-weight:900;color:#4856d6;margin-bottom:0.45rem;">一句话理解</div>
      <p style="margin:0;color:#203247;line-height:1.72;">
        如果一个问题可以拆成连续的小步骤，并且每一步都依赖当前状态，那么它大概率适合用迭代来写。
      </p>
    </div>
  </div>
</div>

<div
  style="
    max-width: 1040px;
    margin: 0.85rem auto 0;
    padding: 0.9rem 1rem;
    border-radius: 20px;
    background: linear-gradient(135deg, rgba(255,241,241,0.98), rgba(255,255,255,0.92));
    border: 1px solid rgba(214,69,69,0.20);
    box-shadow: 0 10px 24px rgba(214,69,69,0.08);
    color: #16273b;
  "
>
  迭代思想的本质：把复杂问题拆成一系列<span style="color:#d64545;font-weight:900;">重复的小步骤</span>。
</div>

---
layout: default
---

# 本节学习目标

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(243,248,247,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <p style="margin:0 0 0.8rem;color:#203247;line-height:1.7;">学完本节后，你应该能回答 4 个问题：</p>
  <div style="display:grid;gap:0.55rem;">
    <div style="padding:0.62rem 0.82rem;border-radius:16px;background:rgba(255,255,255,0.88);border:1px solid rgba(15,118,110,0.12);box-shadow:0 8px 20px rgba(11,36,52,0.05);">1. 什么是<span style="color:#d64545;font-weight:900;">迭代算法</span>？</div>
    <div style="padding:0.62rem 0.82rem;border-radius:16px;background:rgba(255,255,255,0.88);border:1px solid rgba(15,118,110,0.12);box-shadow:0 8px 20px rgba(11,36,52,0.05);">2. 递推法和倒推法有什么区别？</div>
    <div style="padding:0.62rem 0.82rem;border-radius:16px;background:rgba(255,255,255,0.88);border:1px solid rgba(15,118,110,0.12);box-shadow:0 8px 20px rgba(11,36,52,0.05);">3. 如何根据问题建立<span style="color:#d64545;font-weight:900;">迭代关系式</span>？</div>
    <div style="padding:0.62rem 0.82rem;border-radius:16px;background:rgba(255,255,255,0.88);border:1px solid rgba(15,118,110,0.12);box-shadow:0 8px 20px rgba(11,36,52,0.05);">4. 如何用迭代思想求方程的近似根？</div>
  </div>
</div>

<div class="note">
一句话理解：迭代就是从一个已知状态出发，按照固定规则不断更新状态，直到得到目标结果。
</div>

---
layout: default
---

# 本课聚焦：4.1 迭代算法

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(243,248,247,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <p style="margin:0 0 0.8rem;color:#203247;line-height:1.7;">本章内容包括：</p>
  <div style="display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:0.75rem;">
    <div style="padding:0.82rem 0.7rem;border-radius:20px;background:rgba(255,255,255,0.86);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);"><strong style="display:block;font-size:1.08rem;color:#0f766e;">4.1</strong><span style="color:#d64545;font-weight:900;">迭代算法</span> ← 本课重点</div>
    <div style="padding:0.82rem 0.7rem;border-radius:20px;background:rgba(255,255,255,0.86);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);"><strong style="display:block;font-size:1.08rem;color:#0f766e;">4.2</strong>蛮力法</div>
    <div style="padding:0.82rem 0.7rem;border-radius:20px;background:rgba(255,255,255,0.86);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);"><strong style="display:block;font-size:1.08rem;color:#0f766e;">4.3</strong>分而治之算法</div>
    <div style="padding:0.82rem 0.7rem;border-radius:20px;background:rgba(255,255,255,0.86);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);"><strong style="display:block;font-size:1.08rem;color:#0f766e;">4.4</strong>贪婪算法</div>
    <div style="padding:0.82rem 0.7rem;border-radius:20px;background:rgba(255,255,255,0.86);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);"><strong style="display:block;font-size:1.08rem;color:#0f766e;">4.5</strong>动态规划</div>
    <div style="padding:0.82rem 0.7rem;border-radius:20px;background:rgba(255,255,255,0.86);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);"><strong style="display:block;font-size:1.08rem;color:#0f766e;">4.6</strong>算法策略间的比较</div>
  </div>
</div>

<div class="note">
本节主要讨论三类迭代思想：递推法、倒推法、迭代求根。
</div>

---
layout: default
---

# 4.1 迭代算法

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(243,248,247,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <p style="margin:0 0 0.8rem;color:#203247;line-height:1.7;">基本思想：<span style="display:inline-block;padding:0.05rem 0.42rem;border-radius:999px;border:2px solid rgba(214,69,69,0.78);background:rgba(255,241,241,0.82);color:#d64545;font-weight:900;">用旧值计算新值</span>。</p>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:0.9rem;">
    <div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:0.95rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">常用场景</div>
      <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
        <div>1. 数列递推</div>
        <div>2. 状态更新</div>
        <div>3. 数值计算</div>
        <div>4. 方程近似求根</div>
      </div>
    </div>
    <div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.82);border:1px dashed rgba(15,118,110,0.24);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:0.95rem;font-weight:900;color:#0f766e;margin-bottom:0.45rem;">基本步骤</div>
      <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
        <div>1. 确定初始状态</div>
        <div>2. 建立<span style="color:#d64545;font-weight:900;">迭代关系式</span></div>
        <div>3. 重复更新状态</div>
        <div>4. 根据<span style="color:#d64545;font-weight:900;">停止条件</span>结束循环</div>
      </div>
    </div>
  </div>
</div>

---
layout: default
class: text-center
---

# 迭代算法总流程

<div style="max-width:760px;margin:1rem auto 0.9rem;display:grid;gap:0.28rem;justify-items:center;position:relative;">
  <div style="width:2px;position:absolute;top:1rem;bottom:1rem;background:linear-gradient(180deg,rgba(15,118,110,0.24),rgba(201,122,20,0.24));"></div>
  <div style="position:relative;z-index:1;padding:0.36rem 1rem;border-radius:999px;background:rgba(255,255,255,0.92);border:1px solid rgba(15,118,110,0.16);box-shadow:0 8px 20px rgba(11,36,52,0.06);font-weight:800;color:#113a52;">确定初始状态</div>
  <div style="position:relative;z-index:1;width:1.6rem;height:1.6rem;border-radius:999px;background:white;display:flex;align-items:center;justify-content:center;color:#c97a14;font-weight:900;box-shadow:0 8px 20px rgba(11,36,52,0.08);">↓</div>
  <div style="position:relative;z-index:1;padding:0.36rem 1rem;border-radius:999px;background:rgba(255,255,255,0.92);border:1px solid rgba(15,118,110,0.16);box-shadow:0 8px 20px rgba(11,36,52,0.06);font-weight:800;color:#113a52;">建立迭代关系式</div>
  <div style="position:relative;z-index:1;width:1.6rem;height:1.6rem;border-radius:999px;background:white;display:flex;align-items:center;justify-content:center;color:#c97a14;font-weight:900;box-shadow:0 8px 20px rgba(11,36,52,0.08);">↓</div>
  <div style="position:relative;z-index:1;padding:0.36rem 1rem;border-radius:999px;background:rgba(255,255,255,0.92);border:1px solid rgba(15,118,110,0.16);box-shadow:0 8px 20px rgba(11,36,52,0.06);font-weight:800;color:#113a52;">根据旧值计算新值</div>
  <div style="position:relative;z-index:1;width:1.6rem;height:1.6rem;border-radius:999px;background:white;display:flex;align-items:center;justify-content:center;color:#c97a14;font-weight:900;box-shadow:0 8px 20px rgba(11,36,52,0.08);">↓</div>
  <div style="position:relative;z-index:1;padding:0.36rem 1rem;border-radius:999px;background:rgba(255,241,241,0.92);border:1px solid rgba(214,69,69,0.24);box-shadow:0 8px 20px rgba(11,36,52,0.06);font-weight:800;color:#d64545;">判断停止条件</div>
  <div style="position:relative;z-index:1;width:1.6rem;height:1.6rem;border-radius:999px;background:white;display:flex;align-items:center;justify-content:center;color:#c97a14;font-weight:900;box-shadow:0 8px 20px rgba(11,36,52,0.08);">↓</div>
  <div style="position:relative;z-index:1;padding:0.36rem 1rem;border-radius:999px;background:rgba(255,255,255,0.92);border:1px solid rgba(15,118,110,0.16);box-shadow:0 8px 20px rgba(11,36,52,0.06);font-weight:800;color:#113a52;">输出结果</div>
</div>

<div style="max-width:860px;margin:0 auto;padding:0.88rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(233,244,241,0.86));border:1px dashed rgba(15,118,110,0.28);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;">
迭代算法的核心不是某一个公式，而是<span style="color:#d64545;font-weight:900;">状态不断更新</span>的过程。
<div style="margin-top:0.38rem;color:#5f7086;font-size:0.82rem;">↘ 考试、作业、编程实现时，这一句往往就是“本质”。</div>
</div>

---
layout: default
class: text-center
---

# 迭代算法的三种典型形式

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(243,248,247,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <div style="display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:0.85rem;">
    <div style="padding:0.95rem 0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(15,118,110,0.14);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:1rem;font-weight:900;color:#0f766e;margin-bottom:0.25rem;">递推法</div>
      <div style="color:#203247;line-height:1.62;">已知前面，推出后面</div>
      <div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">兔子繁殖、最大公约数</div>
    </div>
    <div style="padding:0.95rem 0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(72,86,214,0.14);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:1rem;font-weight:900;color:#4856d6;margin-bottom:0.25rem;">倒推法</div>
      <div style="color:#203247;line-height:1.62;">已知结果，反推开始</div>
      <div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">猴子吃桃、穿越沙漠</div>
    </div>
    <div style="padding:0.95rem 0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(201,122,20,0.16);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:1rem;font-weight:900;color:#c97a14;margin-bottom:0.25rem;">迭代求根</div>
      <div style="color:#203247;line-height:1.62;">从猜测值出发，逐步逼近</div>
      <div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">牛顿法、二分法</div>
    </div>
  </div>
</div>

<div class="note">
本课主线：先理解“状态如何更新”，再看不同问题中更新方向有什么变化。
</div>

---
layout: default
class: text-center
---

# 递推法

<div style="max-width:980px;margin:0.9rem auto 0;padding:1rem 1.15rem 1.2rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(240,247,245,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <div style="display:inline-block;padding:0.2rem 0.65rem;border-radius:999px;background:rgba(15,118,110,0.10);border:1px solid rgba(15,118,110,0.18);color:#0f766e;font-size:0.78rem;font-weight:800;letter-spacing:0.14em;text-transform:uppercase;">Forward Recurrence</div>
  <div style="margin-top:0.55rem;font-size:1.24rem;font-weight:850;color:#1d3652;">
    递推法：<span style="display:inline-block;padding:0.04rem 0.42rem;border-radius:999px;border:2px solid rgba(214,69,69,0.76);background:rgba(255,241,241,0.82);color:#d64545;">从已知状态出发</span>，一步步推出后续状态。
  </div>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:0.9rem;margin-top:0.9rem;">
    <div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:0.92rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">常见特点</div>
      <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
        <div>1. 已知初始条件</div>
        <div>2. 能写出相邻状态之间的关系</div>
        <div>3. 通过循环不断向后计算</div>
      </div>
    </div>
    <div style="padding:0.95rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(233,244,241,0.86));border:1px dashed rgba(15,118,110,0.26);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;display:flex;align-items:center;justify-content:center;font-size:1.02rem;line-height:1.7;">
      大白话：知道前面怎么算后面。
    </div>
  </div>
</div>

---
layout: default
---

# 4.1.1 递推法：兔子繁殖问题

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(243,248,247,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;line-height:1.72;">
    一对兔子从出生后第三个月开始，每月生一对小兔子。小兔子到第三个月又开始生下一代小兔子。若兔子只生不死，一月份抱来一对刚出生的小兔子，问一年中每个月各有多少<span style="color:#d64545;font-weight:900;">对</span>兔子。
  </div>

  <div style="margin-top:0.85rem;font-size:0.94rem;font-weight:900;color:#113a52;">月份与兔子对数</div>

  <table style="margin-top:0.45rem;">
    <thead>
      <tr><th>月份</th><th>1月</th><th>2月</th><th>3月</th><th>4月</th><th>5月</th></tr>
    </thead>
    <tbody>
      <tr><td>兔子对数</td><td>1</td><td>1</td><td>2</td><td>3</td><td>5</td></tr>
    </tbody>
  </table>

  <div style="margin-top:0.8rem;font-size:0.94rem;font-weight:900;color:#113a52;">数学模型</div>
</div>

$$
y_1 = y_2 = 1,\quad y_n = y_{n-1} + y_{n-2},\quad n \ge 3
$$

<div style="max-width:1040px;margin:0.5rem auto 0;color:#5f7086;font-size:0.84rem;">
<span style="color:#d64545;font-weight:900;">注意</span>：这里是“兔子对数”，不是“兔子只数”。
</div>

---
layout: two-cols
---

# 递推算法 1：每轮生成 1 个新值

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);margin-bottom:0.75rem;">
递推关系：

$$
y_n = y_{n-1} + y_{n-2}
$$
</div>

<div style="padding:0.95rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(255,241,241,0.70));border:1px solid rgba(214,69,69,0.18);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
  <div style="font-size:0.92rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">变量含义</div>
  <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
    <div><code>a</code>：前 2 个月的兔子对数</div>
    <div><code>b</code>：前 1 个月的兔子对数</div>
    <div><code>c</code>：当前月份的兔子对数</div>
  </div>
</div>

<div style="margin-top:0.8rem;font-size:0.92rem;font-weight:900;color:#113a52;">变量更新关系</div>

```text
c = a + b
a = b
b = c
```

::right::

```c
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

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#4856d6;font-weight:900;">关键：</span>每轮只生成一个新值，最直观。
</div>

---
layout: two-cols
---

# 递推算法 2：每轮生成 3 个新值

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
一次循环连续递推 <span style="display:inline-block;padding:0.04rem 0.42rem;border-radius:999px;border:2px solid rgba(214,69,69,0.76);background:rgba(255,241,241,0.82);color:#d64545;font-weight:900;">3 步</span>。
</div>

<div style="margin-top:0.8rem;padding:0.95rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(255,241,241,0.70));border:1px solid rgba(214,69,69,0.18);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
  <div style="font-size:0.92rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">变量更新关系</div>

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

```c
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

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#d64545;font-weight:900;">注意</span>：更新顺序不能乱，初学时优先掌握算法 1。
</div>

---
layout: two-cols
---

# 递推算法 3：每轮生成 2 个新值

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
该写法每轮循环产生 <span style="display:inline-block;padding:0.03rem 0.34rem;border-radius:999px;border:2px solid rgba(214,69,69,0.76);background:rgba(255,241,241,0.82);color:#d64545;font-weight:900;">2 个新值</span>。
</div>

变量更新关系：

```text
a = a + b
b = a + b
```

输出顺序就是：

```text
a, b
```

<div style="margin-top:0.75rem;padding:0.75rem 0.9rem;border-left:6px solid #c97a14;border-radius:0 18px 18px 0;background:linear-gradient(90deg,rgba(201,122,20,0.10),rgba(255,255,255,0.75));color:#344256;font-size:0.88rem;">
三种写法本质相同，都是用前两项推出后一项。
</div>

::right::

```c
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

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#4856d6;font-weight:900;">核心</span>：变量保存的是“当前递推状态”。
</div>

---
layout: default
---

# 递推法：最大公约数

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(243,248,247,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <p style="margin:0;color:#203247;line-height:1.7;">例：求两个整数的最大公约数。</p>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:0.85rem;margin-top:0.8rem;">
    <div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:0.92rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">常见方法</div>
      <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
        <div>1. 短除法</div>
        <div>2. <span style="color:#d64545;font-weight:900;">辗转相除法</span>，也称欧几里得算法</div>
      </div>
    </div>
    <div style="padding:0.95rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(233,244,241,0.86));border:1px dashed rgba(15,118,110,0.26);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;display:flex;align-items:center;justify-content:center;line-height:1.65;">
      每一步都把问题变小，但答案保持不变。
    </div>
  </div>
</div>

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

<div style="max-width:1040px;margin:0.65rem auto 0;padding:0.85rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(233,244,241,0.86));border:1px dashed rgba(15,118,110,0.26);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;">
关键理解：每次把问题变小，但最大公约数不变。
</div>

---
layout: two-cols
---

# 欧几里得算法

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
变量更新关系：

```text
c = a mod b
a = b
b = c
```
</div>

<div style="margin-top:0.8rem;padding:0.95rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(240,244,255,0.86));border:1px solid rgba(72,86,214,0.12);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
  <div style="font-size:0.92rem;font-weight:900;color:#4856d6;margin-bottom:0.45rem;">算法思想</div>
  <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
    <div>1. 每次用余数替换较小问题</div>
    <div>2. 最大公约数不变</div>
    <div>3. 余数最终变为 <span style="color:#d64545;font-weight:900;">0</span></div>
  </div>
</div>

::right::

```c
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

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#4856d6;font-weight:900;">比枚举更强</span>：不断缩小问题规模。
</div>

---
layout: default
class: text-center
---

# 递推法与倒推法对比

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(243,248,247,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <table>
    <thead>
      <tr><th>方法</th><th>推导方向</th><th>已知条件</th><th>典型例子</th></tr>
    </thead>
    <tbody>
      <tr><td><span style="color:#0f766e;font-weight:900;">递推法</span></td><td>从前往后</td><td>初始状态</td><td>兔子繁殖、最大公约数</td></tr>
      <tr><td><span style="color:#4856d6;font-weight:900;">倒推法</span></td><td>从后往前</td><td>最终状态</td><td>猴子吃桃、穿越沙漠</td></tr>
    </tbody>
  </table>
</div>

<div class="mark-box">
判断方法：如果题目给的是“起点”，通常用递推；如果题目给的是“最终结果”，通常考虑倒推。
</div>

---
layout: default
class: text-center
---

# 4.1.2 倒推法

<div style="max-width:980px;margin:0.9rem auto 0;padding:1rem 1.15rem 1.2rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(240,244,255,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <div style="display:inline-block;padding:0.2rem 0.65rem;border-radius:999px;background:rgba(72,86,214,0.10);border:1px solid rgba(72,86,214,0.18);color:#4856d6;font-size:0.78rem;font-weight:800;letter-spacing:0.14em;text-transform:uppercase;">Backward Iteration</div>
  <div style="margin-top:0.55rem;font-size:1.24rem;font-weight:850;color:#1d3652;">
    倒推法：<span style="display:inline-block;padding:0.04rem 0.42rem;border-radius:999px;border:2px solid rgba(214,69,69,0.76);background:rgba(255,241,241,0.82);color:#d64545;">从结果出发</span>，反向恢复初始状态。
  </div>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:0.9rem;margin-top:0.9rem;">
    <div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:0.92rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">常见特点</div>
      <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
        <div>1. 最终状态已知</div>
        <div>2. 正向推导不方便</div>
        <div>3. 反向关系更容易建立</div>
      </div>
    </div>
    <div style="padding:0.95rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(240,244,255,0.86));border:1px dashed rgba(72,86,214,0.22);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;display:flex;align-items:center;justify-content:center;font-size:1.02rem;line-height:1.7;">
      大白话：知道最后变成什么样，再倒着算最开始是什么样。
    </div>
  </div>
</div>

---
layout: two-cols
---

# 倒推法：猴子吃桃

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;line-height:1.72;">
一只小猴子摘了若干桃子，每天吃现有桃的一半多一个。到第 10 天时只剩 1 个桃子，求原有多少个桃？
</div>

<div style="margin-top:0.8rem;font-size:0.92rem;font-weight:900;color:#113a52;">正向关系</div>

```text
第二天桃子数 = 第一天桃子数 / 2 - 1
```

<div style="margin-top:0.8rem;font-size:0.92rem;font-weight:900;color:#113a52;">倒推关系</div>

$$
a_i=(a_{i+1}+1)\times 2,\quad i=9,8,7,\ldots,1
$$

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#4856d6;font-weight:900;">关键</span>：从第 10 天的 1 个桃子开始反推。
</div>

::right::

```c
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

```text
第 10 天：1
第 9 天：(1 + 1) * 2
第 8 天：继续倒推
...
第 1 天：得到原始桃子数
```

---
layout: two-cols
---

# 倒推法：杨辉三角

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;line-height:1.72;">
例：用一维数组输出杨辉三角形。
</div>

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

<div style="margin-top:0.75rem;padding:0.82rem 0.95rem;border-radius:20px;background:linear-gradient(135deg,rgba(255,241,241,0.98),rgba(255,255,255,0.92));border:1px solid rgba(214,69,69,0.20);box-shadow:0 10px 24px rgba(214,69,69,0.08);color:#16273b;">
如果用一维数组，需要避免<span style="color:#d64545;font-weight:900;">新值覆盖旧值</span>。
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

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#d64545;font-weight:900;">重点</span>：从右向左更新。
</div>

---
layout: two-cols
---

# 杨辉三角代码

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
正向错误更新可能产生：

```text
1
1 1
1 2 1
1 3 4 1
1 4 8 9 1
```
</div>

<div style="margin-top:0.8rem;padding:0.95rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(233,244,241,0.86));border:1px dashed rgba(15,118,110,0.26);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
倒向更新可以得到：

```text
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
```
</div>

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#4856d6;font-weight:900;">原因</span>：倒向更新能保留上一行旧值。
</div>

::right::

```c
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

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;line-height:1.72;">
穿越沙漠问题中，起点到底要准备多少油并不直观。
</div>

<div style="margin-top:0.8rem;font-size:0.92rem;font-weight:900;color:#113a52;">但终点附近很清楚</div>

- 最后一段最多只需要 <span class="red">500 加仑</span>油
- 最后一段最多能走 <span class="red">500 公里</span>
- 可以从终点向前反推出每一个储油点

<div style="margin-top:0.75rem;padding:0.9rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(233,244,241,0.86));border:1px dashed rgba(15,118,110,0.26);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;">
所以这个问题从终点开始倒推，比从起点正推更容易建立模型。
</div>

---
layout: two-cols
---

# 倒推法：穿越沙漠

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;line-height:1.72;">
用一辆吉普车穿越 1000 公里的沙漠。吉普车总装油量为 500 加仑，耗油率为 1 加仑/公里。沙漠中没有油库，必须先建立临时油库。
</div>

<div style="margin-top:0.8rem;font-size:0.92rem;font-weight:900;color:#113a52;">最省油方案</div>

- 每次从 `a` 点加满油出发
- `a-b` 之间来回奇数次，最后一次朝 `b` 点走
- `a` 点储油量 = `a-b` 之间耗油量 + `b` 点储油量

::right::

变量说明：

- `k`：从 `a` 加满油向 `b` 出发的次数
- `2k-1`：`a-b` 之间的行驶次数
- `x`：`a-b` 之间距离
- `S1`：`a` 点储油量
- `S2`：`b` 点储油量

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

```text
起点 ---- 储油点 a ---- 储油点 b ---- 终点
          S1 = 500k       S2
          距离 x
          行驶 2k - 1 次
```

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#d64545;font-weight:900;">圈重点</span>：倒推时先看离终点最近的一段。
</div>

---
layout: two-cols
---

# 沙漠问题代码

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
程序输出：

<ul>
  <li>储油点序号</li>
  <li>储油点距离</li>
  <li>储油量</li>
</ul>
</div>

<div style="margin-top:0.75rem;padding:0.82rem 0.95rem;border-radius:20px;background:linear-gradient(135deg,rgba(255,241,241,0.98),rgba(255,255,255,0.92));border:1px solid rgba(214,69,69,0.20);box-shadow:0 10px 24px rgba(214,69,69,0.08);color:#16273b;">
注意：该问题涉及非整数距离，应使用 <span style="color:#d64545;font-weight:900;">double</span> 类型。
</div>

::right::

```c
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

<div style="max-width:980px;margin:0.9rem auto 0;padding:1rem 1.15rem 1.2rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(255,247,238,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <div style="display:inline-block;padding:0.2rem 0.65rem;border-radius:999px;background:rgba(201,122,20,0.10);border:1px solid rgba(201,122,20,0.18);color:#c97a14;font-size:0.78rem;font-weight:800;letter-spacing:0.14em;text-transform:uppercase;">Numerical Iteration</div>
  <div style="margin-top:0.55rem;font-size:1.24rem;font-weight:850;color:#1d3652;">
    迭代求根：<span style="display:inline-block;padding:0.04rem 0.42rem;border-radius:999px;border:2px solid rgba(214,69,69,0.76);background:rgba(255,241,241,0.82);color:#d64545;">从一个猜测值出发</span>，不断逼近真实解。
  </div>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:0.9rem;margin-top:0.9rem;">
    <div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:0.92rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">常见方法</div>
      <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
        <div>1. 牛顿迭代法</div>
        <div>2. 二分法</div>
      </div>
    </div>
    <div style="padding:0.95rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(255,247,238,0.86));border:1px dashed rgba(201,122,20,0.24);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;display:flex;align-items:center;justify-content:center;font-size:1.02rem;line-height:1.7;">
      大白话：先猜一个答案，再用规则不断修正它。
    </div>
  </div>
</div>

---
layout: default
---

# 迭代法解方程：基本框架

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(255,247,238,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <p style="margin:0;color:#203247;line-height:1.7;">很多方程难以直接求出精确解，可以通过迭代获得近似解。</p>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:0.85rem;margin-top:0.85rem;">
    <div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:0.92rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">基本步骤</div>
      <div style="display:grid;gap:0.38rem;color:#203247;line-height:1.62;">
        <div>1. 确定初值 $x_0$</div>
        <div>2. 建立迭代关系：由 $f(x)=0$ 转换为 $x=\varphi(x)$</div>
        <div>3. 构造数列：$x_n=\varphi(x_{n-1})$</div>
        <div>4. 当误差小于精度要求时停止</div>
      </div>
    </div>
    <div style="padding:0.95rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(255,247,238,0.86));border:1px dashed rgba(201,122,20,0.24);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;line-height:1.62;">
      迭代流程可以理解为：
      <div style="margin-top:0.45rem;display:grid;gap:0.3rem;">
        <div>1. 选择初始值 <code>x0</code></div>
        <div>2. 计算新值 <code>x1</code></div>
        <div>3. 判断误差是否足够小</div>
        <div>4. 若不满足，令 <code>x0 = x1</code> 继续迭代</div>
        <div>5. 若满足，输出近似根</div>
      </div>
    </div>
  </div>
</div>
<div style="max-width:1040px;margin:0.55rem auto 0;color:#5f7086;font-size:0.84rem;">
<span style="color:#4856d6;font-weight:900;">关键</span>：初值、迭代关系、停止条件缺一不可。
</div>

---
layout: default
---

# 迭代法求方程组根

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(255,247,238,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:0.85rem;">
    <div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
      <div style="font-size:0.92rem;font-weight:900;color:#113a52;margin-bottom:0.45rem;">已知初值</div>
      <div style="color:#203247;line-height:1.62;">$X=(x_0,x_1,\ldots,x_{n-1})$</div>
      <div style="margin-top:0.75rem;font-size:0.92rem;font-weight:900;color:#113a52;">迭代关系方程组</div>
      <div style="color:#203247;line-height:1.62;">$x_i=g_i(X),\quad i=0,1,\ldots,n-1$</div>
      <div style="margin-top:0.4rem;color:#203247;">其中 <code>w</code> 为解的精度。</div>
    </div>
  </div>
</div>

```c
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

<div style="max-width:1040px;margin:0.55rem auto 0;color:#5f7086;font-size:0.84rem;">
<span style="color:#d64545;font-weight:900;">注意</span>：每轮迭代前误差累计量 <code>c</code> 要清零。
</div>

---
layout: two-cols
---

# 牛顿迭代法求根

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
目标：求形如

$$
ax^3+bx^2+cx+d=0
$$

的方程根。
</div>

<div style="margin-top:0.8rem;font-size:0.92rem;font-weight:900;color:#113a52;">牛顿迭代思想：用切线近似曲线</div>

$$
f(x_0)+f'(x_0)(x-x_0)\approx 0
$$

因此：

$$
x_1=x_0-\frac{f(x_0)}{f'(x_0)}
$$

::right::

```text
初值 x0
  ↓
计算 f(x0) 与 f'(x0)
  ↓
x1 = x0 - f(x0) / f'(x0)
  ↓
判断 |x1 - x0| 是否小于精度
```

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#4856d6;font-weight:900;">本质</span>：用切线交点更新下一次近似值。
</div>

---
layout: two-cols
---

# 牛顿迭代代码

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
示例：

$$
x^3+2x^2+3x+4=0
$$

停止条件：

$$
|x_1-x_0|<10^{-4}
$$
</div>

::right::

```c
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

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#d64545;font-weight:900;">快</span>：牛顿法收敛快，但需要求导，而且对初值较敏感。
</div>

---
layout: two-cols
---

# 二分法求方程根

<div style="padding:0.95rem 1rem;border-radius:22px;background:rgba(255,255,255,0.88);border:1px solid rgba(17,58,82,0.08);box-shadow:0 10px 24px rgba(11,36,52,0.06);">
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
</div>

::right::

二分法前提：

- $f(x)$ 在区间 $[a,b]$ 上连续
- $f(a)$ 与 $f(b)$ <span class="red">异号</span>

基本思想：

```text
每次取中点 c = (a + b) / 2
保留仍然存在根的一半区间
```

<div style="margin-top:0.55rem;color:#5f7086;font-size:0.84rem;">
<span style="color:#d64545;font-weight:900;">重点</span>：二分法必须先保证区间两端异号。
</div>

---
layout: two-cols
---

# 二分法代码

停止条件：函数值足够接近 0。

$$
|f(x)|<10^{-4}
$$

<div style="margin-top:0.75rem;padding:0.82rem 0.95rem;border-radius:20px;background:linear-gradient(135deg,rgba(255,241,241,0.98),rgba(255,255,255,0.92));border:1px solid rgba(214,69,69,0.20);box-shadow:0 10px 24px rgba(214,69,69,0.08);color:#16273b;">
二分法特点：<span style="color:#d64545;font-weight:900;">稳定可靠</span>，但收敛速度比牛顿法慢。
</div>

::right::

```c
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

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.15rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(243,248,247,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <table>
    <thead>
      <tr><th>方法</th><th>优点</th><th>缺点</th><th>适用情况</th></tr>
    </thead>
    <tbody>
      <tr><td><span style="color:#0f766e;font-weight:900;">牛顿法</span></td><td>收敛速度快</td><td>需要求导，对初值敏感</td><td>函数可导，初值较好</td></tr>
      <tr><td><span style="color:#c97a14;font-weight:900;">二分法</span></td><td>稳定可靠</td><td>收敛速度较慢</td><td>已知根所在区间</td></tr>
    </tbody>
  </table>
</div>

<div style="max-width:1040px;margin:0.7rem auto 0;padding:0.9rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(233,244,241,0.86));border:1px dashed rgba(15,118,110,0.24);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;">
选择建议：能求导且初值较好，用牛顿法；只知道根所在区间，用二分法。
</div>

---
layout: default
class: text-center
---

# 小结

<div style="max-width:1040px;margin:0.8rem auto 0;padding:1rem 1.1rem 1.2rem;border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,0.98),rgba(243,248,247,0.96));border:1px solid rgba(17,58,82,0.10);box-shadow:0 18px 50px rgba(11,36,52,0.10);">
  <p style="margin:0 0 0.8rem;color:#203247;line-height:1.7;">迭代算法的关键是：</p>
  <div style="margin-bottom:0.9rem;color:#1d3652;font-size:1.1rem;font-weight:850;">
    <span style="display:inline-block;padding:0.05rem 0.4rem;border-radius:999px;border:2px solid rgba(214,69,69,0.72);background:rgba(255,241,241,0.82);color:#d64545;">初值</span>
    、<span style="display:inline-block;padding:0.05rem 0.4rem;border-radius:999px;border:2px solid rgba(214,69,69,0.72);background:rgba(255,241,241,0.82);color:#d64545;">关系式</span>
    、<span style="display:inline-block;padding:0.05rem 0.4rem;border-radius:999px;border:2px solid rgba(214,69,69,0.72);background:rgba(255,241,241,0.82);color:#d64545;">更新过程</span>
    、<span style="display:inline-block;padding:0.05rem 0.4rem;border-radius:999px;border:2px solid rgba(214,69,69,0.72);background:rgba(255,241,241,0.82);color:#d64545;">停止条件</span>
  </div>
  <table>
    <thead>
      <tr><th>类型</th><th>一句话总结</th></tr>
    </thead>
    <tbody>
      <tr><td>递推法</td><td>知道前面，推出后面</td></tr>
      <tr><td>倒推法</td><td>知道结果，反推开始</td></tr>
      <tr><td>迭代求根</td><td>从猜测值出发，逐步逼近真实解</td></tr>
    </tbody>
  </table>
</div>

<div style="max-width:1040px;margin:0.75rem auto 0;padding:0.9rem 1rem;border-radius:20px;background:linear-gradient(135deg,rgba(255,241,241,0.98),rgba(255,255,255,0.92));border:1px solid rgba(214,69,69,0.20);box-shadow:0 10px 24px rgba(214,69,69,0.08);color:#16273b;">
迭代算法的本质不是公式堆砌，而是把复杂问题拆成一次又一次的<span style="color:#d64545;font-weight:900;">状态更新</span>。
</div>

<div style="max-width:1040px;margin:0.75rem auto 0;padding:0.9rem 1rem;border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,0.96),rgba(233,244,241,0.86));border:1px dashed rgba(15,118,110,0.24);box-shadow:0 10px 24px rgba(11,36,52,0.06);color:#203247;line-height:1.7;">
学完这一章，真正要带走的不是几个例题，而是一个统一框架：先找<span style="color:#d64545;font-weight:900;">当前状态</span>，再写出<span style="color:#d64545;font-weight:900;">更新规则</span>，最后设定<span style="color:#d64545;font-weight:900;">结束条件</span>。
</div>

<div style="display:inline-block;margin-top:0.9rem;padding:0.2rem 0.7rem;border-radius:999px;background:rgba(15,118,110,0.10);border:1px solid rgba(15,118,110,0.18);color:#0f766e;font-size:0.8rem;font-weight:800;letter-spacing:0.14em;text-transform:uppercase;">Iteration Is Controlled Change</div>
