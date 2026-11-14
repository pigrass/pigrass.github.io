>引用: https://www.markdownassistant.com/zh/math

LaTeX/KaTeX 数学公式语法指南：行内公式与块级公式的写法，以及分数、上下标、根号、矩阵、积分、求和、希腊字母等常用符号的用法，每例均有实时渲染效果。

## 行内公式与块级公式

### 行内公式 (Inline Math)

在 Markdown 中，使用单个 `$` 符号包裹 LaTeX 公式即可插入**行内公式**。

**源码：**

```markdown
爱因斯坦的质能方程 $E = mc^2$ 是物理学中最著名的公式之一。
勾股定理可以表示为 $a^2 + b^2 = c^2$。
圆的面积公式为 $A = \pi r^2$。
```

**渲染效果：**

爱因斯坦的质能方程 $E = mc^2$ 是物理学中最著名的公式之一。
勾股定理可以表示为 $a^2 + b^2 = c^2$。
圆的面积公式为 $A = \pi r^2$。

行内公式会与文字在同一行中显示，适合在段落中嵌入简短的数学表达式。

---
### 块级公式 (Block Math)

使用双 `$$` 符号包裹 LaTeX 公式可以创建**块级公式**，公式会独占一行居中显示。

**源码：**

```markdown
$$
E = mc^2
$$

$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$
```

**渲染效果：**

$$
E = mc^2
$$

$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$

块级公式适合展示较长或需要突出显示的数学表达式。

---

## 基本运算符

### 加减乘除与幂运算

LaTeX 支持常见的数学运算符。

**源码：**

```markdown
**加减法**：$a + b$、$a - b$

**乘法**：$a \times b$、$a \cdot b$

**除法**：$a \div b$

**幂运算**：$x^2$、$x^3$、$2^{10}$

**取模**：$a \mod b$

$$
(x + y)^2 = x^2 + 2xy + y^2
$$
```

**渲染效果：**

**加减法**：$a + b$、$a - b$

**乘法**：$a \times b$、$a \cdot b$

**除法**：$a \div b$

**幂运算**：$x^2$、$x^3$、$2^{10}$

**取模**：$a \mod b$

$$
(x + y)^2 = x^2 + 2xy + y^2
$$

---

### 比较运算符

常用比较运算符。

**源码：**

```markdown
- 等于：$a = b$
- 不等于：$a \neq b$
- 大于：$a > b$
- 小于：$a < b$
- 大于等于：$a \geq b$
- 小于等于：$a \leq b$
- 约等于：$a \approx b$
- 相当于：$a \equiv b$
```

**渲染效果：**

- 等于：$a = b$
- 不等于：$a \neq b$
- 大于：$a > b$
- 小于：$a < b$
- 大于等于：$a \geq b$
- 小于等于：$a \leq b$
- 约等于：$a \approx b$
- 相当于：$a \equiv b$

---

## 分数与根式

### 分数 (Fractions)

使用 `\frac{分子}{分母}` 创建分数。

**源码：**

```markdown
简单分数：$\frac{1}{2}$、$\frac{3}{4}$

复杂分数：$\frac{a+b}{c-d}$

$$
\frac{1}{1+\frac{1}{1+\frac{1}{2}}}
$$

使用 `\dfrac` 可以让行内分数更大：$\dfrac{a}{b}$ vs $\frac{a}{b}$
```

**渲染效果：**

简单分数：$\frac{1}{2}$、$\frac{3}{4}$

复杂分数：$\frac{a+b}{c-d}$

$$
\frac{1}{1+\frac{1}{1+\frac{1}{2}}}
$$

使用 `\dfrac` 可以让行内分数更大：$\dfrac{a}{b}$ vs $\frac{a}{b}$

---

### 根式 (Roots)

使用 `\sqrt{}` 创建平方根，`\sqrt[n]{ }` 创建 n 次方根。

**源码：**

```markdown
平方根：$\sqrt{2}$、$\sqrt{x^2 + y^2}$

n 次方根：$\sqrt[3]{8}$、$\sqrt[n]{x}$

$$
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$
```

**渲染效果：**

平方根：$\sqrt{2}$、$\sqrt{x^2 + y^2}$

n 次方根：$\sqrt[3]{8}$、$\sqrt[n]{x}$

$$
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$

这就是著名的**一元二次方程求根公式**。

---

## 上下标

### 上标 (Superscripts)

使用 `^` 创建上标。

**源码：**

```markdown
$x^2$、$x^3$、$x^{n+1}$

多字符上标需要花括号：$x^{10}$

- 指数：$e^{x}$
- 幂：$2^{32}$
- 转置：$A^{T}$
- 导数：$f^{\prime}(x)$、$f^{\prime\prime}(x)$
```

**渲染效果：**

$x^2$、$x^3$、$x^{n+1}$

多字符上标需要花括号：$x^{10}$

- 指数：$e^{x}$
- 幂：$2^{32}$
- 转置：$A^{T}$
- 导数：$f^{\prime}(x)$、$f^{\prime\prime}(x)$

---

### 下标 (Subscripts)

使用 `_` 创建下标。

**源码：**

```markdown
$x_1$、$x_2$、$x_{i,j}$

多字符下标需要花括号：$a_{max}$

- 序号：$x_1, x_2, \ldots, x_n$
- 矩阵元素：$a_{ij}$
- 偏导：$f_{x}$

上下标组合使用：$x_1^2$、$a_{i}^{n}$
```

**渲染效果：**

$x_1$、$x_2$、$x_{i,j}$

多字符下标需要花括号：$a_{max}$

- 序号：$x_1, x_2, \ldots, x_n$
- 矩阵元素：$a_{ij}$
- 偏导：$f_{x}$

上下标组合使用：$x_1^2$、$a_{i}^{n}$

---

## 希腊字母

### 常用希腊字母

LaTeX 提供了完整的希腊字母支持。

**源码：**

```markdown
**小写字母**：
$\alpha$、$\beta$、$\gamma$、$\delta$、$\epsilon$、$\zeta$、$\eta$、$\theta$、$\lambda$、$\mu$、$\nu$、$\xi$、$\pi$、$\rho$、$\sigma$、$\tau$、$\phi$、$\chi$、$\psi$、$\omega$

**大写字母**：
$\Gamma$、$\Delta$、$\Theta$、$\Lambda$、$\Xi$、$\Pi$、$\Sigma$、$\Phi$、$\Psi$、$\Omega$

**变体形式**：
$\varepsilon$（变体 epsilon）、$\vartheta$（变体 theta）、$\varphi$（变体 phi）
```

**渲染效果：**

**小写字母**：
$\alpha$、$\beta$、$\gamma$、$\delta$、$\epsilon$、$\zeta$、$\eta$、$\theta$、$\lambda$、$\mu$、$\nu$、$\xi$、$\pi$、$\rho$、$\sigma$、$\tau$、$\phi$、$\chi$、$\psi$、$\omega$

**大写字母**：
$\Gamma$、$\Delta$、$\Theta$、$\Lambda$、$\Xi$、$\Pi$、$\Sigma$、$\Phi$、$\Psi$、$\Omega$

**变体形式**：
$\varepsilon$（变体 epsilon）、$\vartheta$（变体 theta）、$\varphi$（变体 phi）

---

### 希腊字母应用示例

希腊字母在数学公式中广泛应用。

**源码：**

```markdown
**物理学**：
$F = ma$（力）、$\omega = 2\pi f$（角频率）、$\lambda$（波长）、$\rho$（密度）

**微积分**：
$\delta$（变分符号）、$\epsilon$-$\delta$ 定义

**概率统计**：
$\mu$（均值）、$\sigma$（标准差）、$\Omega$（样本空间）

$$
\Delta x = x_2 - x_1
$$
```

**渲染效果：**

**物理学**：
$F = ma$（力）、$\omega = 2\pi f$（角频率）、$\lambda$（波长）、$\rho$（密度）

**微积分**：
$\delta$（变分符号）、$\epsilon$-$\delta$ 定义

**概率统计**：
$\mu$（均值）、$\sigma$（标准差）、$\Omega$（样本空间）

$$
\Delta x = x_2 - x_1
$$

---

## 求和与积分

### 求和与连乘

**源码：**

```markdown
**求和符号** `\sum`：

$$
\sum_{i=1}^{n} i^2 = \frac{n(n+1)(2n+1)}{6}
$$

**连乘符号** `\prod`：

$$
n! = \prod_{i=1}^{n} i
$$

**极限** `\lim`：

$$
\lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^n = e
$$

行内写法：$\sum_{i=1}^{n} i$、$\prod_{k=1}^{n} k$、$\lim_{x \to 0} f(x)$
```

**渲染效果：**

**求和符号** `\sum`：

$$
\sum_{i=1}^{n} i^2 = \frac{n(n+1)(2n+1)}{6}
$$

**连乘符号** `\prod`：

$$
n! = \prod_{i=1}^{n} i
$$

**极限** `\lim`：

$$
\lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^n = e
$$

行内写法：$\sum_{i=1}^{n} i$、$\prod_{k=1}^{n} k$、$\lim_{x \to 0} f(x)$

---

### 积分 (Integrals)

**源码：**

```markdown
**不定积分**：

$$
\int x^2 \, dx = \frac{x^3}{3} + C
$$

**定积分**：

$$
\int_{0}^{1} x^2 \, dx = \frac{1}{3}
$$

**多重积分**：

$$
\iint_D f(x,y) \, dx \, dy
$$

$$
\iiint_V f(x,y,z) \, dx \, dy \, dz
$$

**曲线/曲面积分**：

$$
\oint_C \vec{F} \cdot d\vec{r}
$$
```

**渲染效果：**

**不定积分**：

$$
\int x^2 \, dx = \frac{x^3}{3} + C
$$

**定积分**：

$$
\int_{0}^{1} x^2 \, dx = \frac{1}{3}
$$

**多重积分**：

$$
\iint_D f(x,y) \, dx \, dy
$$

$$
\iiint_V f(x,y,z) \, dx \, dy \, dz
$$

**曲线/曲面积分**：

$$
\oint_C \vec{F} \cdot d\vec{r}
$$

---

## 矩阵

### 基本矩阵

使用 `\begin{matrix}` 创建无括号矩阵。

**源码：**

```markdown
无括号矩阵：

$$
\begin{matrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
$$

圆括号矩阵 `\begin{pmatrix}`：

$$
\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}
$$

方括号矩阵 `\begin{bmatrix}`：

$$
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
$$
```

**渲染效果：**

无括号矩阵：

$$
\begin{matrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
$$

圆括号矩阵 `\begin{pmatrix}`：

$$
\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}
$$

方括号矩阵 `\begin{bmatrix}`：

$$
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
$$

---

### 更多矩阵样式与行列式

**源码：**

```markdown
**花括号矩阵** `\begin{Bmatrix}`：

$$
\begin{Bmatrix}
a & b \\
c & d
\end{Bmatrix}
$$

**行列式** `\begin{vmatrix}`：

$$
\begin{vmatrix}
a & b \\
c & d
\end{vmatrix} = ad - bc
$$

**省略号矩阵**：

$$
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
$$
```

**渲染效果：**

**花括号矩阵** `\begin{Bmatrix}`：

$$
\begin{Bmatrix}
a & b \\
c & d
\end{Bmatrix}
$$

**行列式** `\begin{vmatrix}`：

$$
\begin{vmatrix}
a & b \\
c & d
\end{vmatrix} = ad - bc
$$

**省略号矩阵**：

$$
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
$$

---

## 方程与对齐

### 多行方程对齐

使用 `align` 环境对齐多行方程，`&` 指定对齐位置。

**源码：**

```markdown
$$
\begin{align}
f(x) &= x^2 + 2x + 1 \\
&= (x+1)^2
\end{align}
$$

多步骤推导：

$$
\begin{align}
(a+b)^2 &= (a+b)(a+b) \\
&= a^2 + ab + ba + b^2 \\
&= a^2 + 2ab + b^2
\end{align}
$$
```

**渲染效果：**

$$
\begin{align}
f(x) &= x^2 + 2x + 1 \\
&= (x+1)^2
\end{align}
$$

多步骤推导：

$$
\begin{align}
(a+b)^2 &= (a+b)(a+b) \\
&= a^2 + ab + ba + b^2 \\
&= a^2 + 2ab + b^2
\end{align}
$$

---

### 方程组

使用 `cases` 环境创建分段函数或方程组。

**源码：**

```markdown
**分段函数**：

$$
f(x) = \begin{cases}
x^2 & \text{if } x \geq 0 \\
-x^2 & \text{if } x < 0
\end{cases}
$$

**方程组**：

$$
\begin{cases}
x + y = 5 \\
2x - y = 1
\end{cases}
$$

**绝对值函数**：

$$
|x| = \begin{cases}
x & x \geq 0 \\
-x & x < 0
\end{cases}
$$
```

**渲染效果：**

**分段函数**：

$$
f(x) = \begin{cases}
x^2 & \text{if } x \geq 0 \\
-x^2 & \text{if } x < 0
\end{cases}
$$

**方程组**：

$$
\begin{cases}
x + y = 5 \\
2x - y = 1
\end{cases}
$$

**绝对值函数**：

$$
|x| = \begin{cases}
x & x \geq 0 \\
-x & x < 0
\end{cases}
$$

---

## 常用数学符号

### 集合与逻辑符号

**源码：**

```markdown
**集合符号**：

- 属于：$x \in A$
- 不属于：$x \notin A$
- 子集：$A \subset B$、$A \subseteq B$
- 真子集：$A \subsetneq B$
- 并集：$A \cup B$
- 交集：$A \cap B$
- 空集：$\emptyset$ 或 $\varnothing$
- 全集：$\mathbb{U}$

**逻辑符号**：

- 且：$p \land q$
- 或：$p \lor q$
- 非：$\neg p$
- 推出：$p \Rightarrow q$
- 等价：$p \Leftrightarrow q$
- 任意：$\forall$
- 存在：$\exists$
```

**渲染效果：**

**集合符号**：

- 属于：$x \in A$
- 不属于：$x \notin A$
- 子集：$A \subset B$、$A \subseteq B$
- 真子集：$A \subsetneq B$
- 并集：$A \cup B$
- 交集：$A \cap B$
- 空集：$\emptyset$ 或 $\varnothing$
- 全集：$\mathbb{U}$

**逻辑符号**：

- 且：$p \land q$
- 或：$p \lor q$
- 非：$\neg p$
- 推出：$p \Rightarrow q$
- 等价：$p \Leftrightarrow q$
- 任意：$\forall$
- 存在：$\exists$

---

### 箭头与特殊符号

**源码：**

```markdown
**箭头**：

- 右箭头：$\rightarrow$ 或 $\to$
- 左箭头：$\leftarrow$
- 双向箭头：$\leftrightarrow$
- 长箭头：$\Longrightarrow$
- 映射箭头：$\mapsto$

**特殊符号**：

- 无穷大：$\infty$
- 偏导：$\partial$
- 纳布拉（梯度算子）：$\nabla$
- 正负号：$\pm$、$\mp$
- 省略号：$\ldots$、$\cdots$、$\vdots$、$\ddots$
- 度数：$30^\circ$
- 角度：$\angle ABC$
```

**渲染效果：**

**箭头**：

- 右箭头：$\rightarrow$ 或 $\to$
- 左箭头：$\leftarrow$
- 双向箭头：$\leftrightarrow$
- 长箭头：$\Longrightarrow$
- 映射箭头：$\mapsto$

**特殊符号**：

- 无穷大：$\infty$
- 偏导：$\partial$
- 纳布拉（梯度算子）：$\nabla$
- 正负号：$\pm$、$\mp$
- 省略号：$\ldots$、$\cdots$、$\vdots$、$\ddots$
- 度数：$30^\circ$
- 角度：$\angle ABC$

---

## 高级用法

### 括号与定界符

LaTeX 提供多种括号，使用 `\left` 和 `\right` 自动调整大小。

**源码：**

```markdown
**手动大小**：
$(\frac{a}{b})$ vs $\left(\frac{a}{b}\right)$

**括号类型**：

- 圆括号：$\left( \frac{a}{b} \right)$
- 方括号：$\left[ \frac{a}{b} \right]$
- 花括号：$\left\{ \frac{a}{b} \right\}$
- 尖括号：$\left\langle \frac{a}{b} \right\rangle$
- 绝对值：$\left| \frac{a}{b} \right|$
- 范数：$\left\| \vec{v} \right\|$

**单侧括号**：
$\left. \frac{dy}{dx} \right|_{x=1}$
```

**渲染效果：**

**手动大小**：
$(\frac{a}{b})$ vs $\left(\frac{a}{b}\right)$

**括号类型**：

- 圆括号：$\left( \frac{a}{b} \right)$
- 方括号：$\left[ \frac{a}{b} \right]$
- 花括号：$\left\lbrace \frac{a}{b} \right\rbrace$
- 尖括号：$\left\langle \frac{a}{b} \right\rangle$
- 绝对值：$\left| \frac{a}{b} \right|$
- 范数：$\left\| \vec{v} \right\|$

**单侧括号**：
$\left. \frac{dy}{dx} \right|_{x=1}$

---

### 字体与函数名

**源码：**

```markdown
**数学字体**：

- 粗体：$\mathbf{A}$（向量/矩阵）
- 花体：$\mathbb{R}$（实数集）、$\mathbb{N}$（自然数集）
- 斜体：$\mathit{x}$（变量）
- 罗马体：$\mathrm{d}x$（微分符号）
- 哥特体：$\mathfrak{g}$

**常用函数名**（正体显示）：
$\sin x$、$\cos x$、$\tan x$
$\log x$、$\ln x$、$\exp(x)$
$\max(a,b)$、$\min(a,b)$
$\det(A)$、$\dim(V)$

向量：
$\vec{a}$、$\mathbf{a}$、$\hat{x}$
```

**渲染效果：**

**数学字体**：

- 粗体：$\mathbf{A}$（向量/矩阵）
- 花体：$\mathbb{R}$（实数集）、$\mathbb{N}$（自然数集）
- 斜体：$\mathit{x}$（变量）
- 罗马体：$\mathrm{d}x$（微分符号）
- 哥特体：$\mathfrak{g}$

**常用函数名**（正体显示）：
$\sin x$、$\cos x$、$\tan x$
$\log x$、$\ln x$、$\exp(x)$
$\max(a,b)$、$\min(a,b)$
$\det(A)$、$\dim(V)$

向量：
$\vec{a}$、$\mathbf{a}$、$\hat{x}$

---

### 空格与排版技巧

LaTeX 数学模式中的空格控制。

**源码：**

```markdown
- 无空格：$ab$
- 小空格：$a\,b$
- 中等空格：$a\;b$
- 大空格：$a\quad b$
- 超大空格：$a\qquad b$

在积分中添加空格：

$$
\int_0^1 x^2 \, dx \quad \text{vs} \quad \int_0^1 x^2 dx
$$

使用 `\text{}` 在公式中插入文字：

$$
\text{当 } x > 0 \text{ 时，有 } f(x) = \sqrt{x}
$$

使用 `\color{}` 改变颜色（部分支持）：

$$
\textcolor{red}{E} = mc^2
$$
```

**渲染效果：**

- 无空格：$ab$
- 小空格：$a\,b$
- 中等空格：$a\;b$
- 大空格：$a\quad b$
- 超大空格：$a\qquad b$

在积分中添加空格：

$$
\int_0^1 x^2 \, dx \quad \text{vs} \quad \int_0^1 x^2 dx
$$

使用 `\text{}` 在公式中插入文字：

$$
\text{当 } x > 0 \text{ 时，有 } f(x) = \sqrt{x}
$$

使用 `\color{}` 改变颜色（部分支持）：

$$
\textcolor{red}{E} = mc^2
$$

---

## 实用技巧

### 常见物理与数学公式

**源码：**

```markdown
**牛顿第二定律**：

$$
\vec{F} = m\vec{a} = m\frac{d\vec{v}}{dt}
$$

**薛定谔方程**：

$$
i\hbar\frac{\partial}{\partial t}\Psi(\vec{r},t) = \hat{H}\Psi(\vec{r},t)
$$

**欧拉公式**：

$$
e^{i\pi} + 1 = 0
$$

**泰勒展开**：

$$
f(x) = \sum_{n=0}^{\infty} \frac{f^{(n)}(a)}{n!}(x-a)^n
$$

**高斯积分**：

$$
\int_{-\infty}^{\infty} e^{-x^2} \, dx = \sqrt{\pi}
$$
```

**渲染效果：**

**牛顿第二定律**：

$$
\vec{F} = m\vec{a} = m\frac{d\vec{v}}{dt}
$$

**薛定谔方程**：

$$
i\hbar\frac{\partial}{\partial t}\Psi(\vec{r},t) = \hat{H}\Psi(\vec{r},t)
$$

**欧拉公式**：

$$
e^{i\pi} + 1 = 0
$$

**泰勒展开**：

$$
f(x) = \sum_{n=0}^{\infty} \frac{f^{(n)}(a)}{n!}(x-a)^n
$$

**高斯积分**：

$$
\int_{-\infty}^{\infty} e^{-x^2} \, dx = \sqrt{\pi}
$$

---

### 编写技巧与注意事项

**1. 特殊字符转义**

在 LaTeX 中，以下字符需要转义：`# $ % & _ { }`
使用反斜杠转义：`\#`、`\$`、`\%`、`\&`、`\_`

**2. 长公式换行**

使用 `\\` 在 align 环境中换行：

**源码：**

```markdown
$$
\begin{align}
y &= a_0 + a_1x + a_2x^2 \\
&\quad + a_3x^3 + a_4x^4
\end{align}
$$
```

**渲染效果：**

$$
\begin{align}
y &= a_0 + a_1x + a_2x^2 \\
&\quad + a_3x^3 + a_4x^4
\end{align}
$$

---

**3. 多行公式编号**

使用 `\tag{}` 自定义编号。

**源码：**

```markdown
$$
a^n + b^n = c^n \tag{1}
$$
```

**渲染效果：**

$$
a^n + b^n = c^n \tag{1}
$$

**4. 行内公式建议**

对于行内公式，较复杂的表达式建议使用块级公式以获得更好的可读性。

---

> 💡 **提示**：如需查阅更多 LaTeX 符号，可参考 [KaTeX 官方文档](https://katex.org/docs/supported)。


  