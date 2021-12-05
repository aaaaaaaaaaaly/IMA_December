# 📈LaTex学习

## 前情

还未配置tex

用在线编辑的 **overleaf** 练习:

学习参考文档：

[]: https://liam.page/2014/09/08/latex-introduction/	"（ctrl+点击链接）"

## 正文

### 简单语法

```
\documentclass{artical}
.....导言部分，通常用来设置页面大小，页眉页脚样式，章节标题式.....
\begin{document}
....................正文部分
\end{document}     
```

其中，**\documentclass{artical}**包含控制序列，会通过{}中的参数来影响文档的效果。比如此处表明调用名为 artical 的文档类

```
% 是注释标记

[]包括的可选参数 也可以是控制序列

\是转义字符

如果想要在正常的内容里显示%，使用 \% 即可

\end{document} 之后插入的任何内容都是无效的
```

### 中英混排

概念: 宏包：一系列控制序列的合集

```
\usepackage{}  -->  可以用来调用宏包
```

介绍了使用 CTeX宏集 来处理中英混排

```
//在编辑框输入
\documentclass[UTF8]{ctexart}
\begin{document}
你好，world!
\end{document}

文档类别从 article 变成 ctexart
增加了选项 [UTF8]

```

```
\documentclass{article}
\usepackage{xeCJK} %调用 xeCJK 宏包
\setCJKmainfont{SimSun} %设置 CJK 主字体为 SimSun （宋体）
...............导言的设置部分........
\begin{document}
你好，world!
\end{document}
```

###  文章编辑

#### 作者，标题，日期

```
\documentclass[UTF8]{ctexart}

\title{你好，world!}.....................标题
\author{Liam}...........................作者
\date{\today}...........................日期

\begin{document}
\maketitle...........................控制序列
你好，world!
\end{document}

\maketitle 是一个控制序列，能将标题，作者，日期按照预定格式展现
```

#### 章节和段落

```
\begin{document}
\maketitle

\section{}
\subsection{}
\subsubsection{}
....用于划分不同part并且通过section，subsection来划分层次

\section{第一章}
  你好，世界！
    \subsection{第一节}
    这是第一节
  \section{第二章}
  这是第二章
  
\paragraph{}
\subparagraph{}

\end{document}

.....................tips............................

\section{ }和\paragraph{ }，功能相似，但是\section{ }会自动编号，也会在目录中自动显示
\paragraph{ }不会自动编号，也不会再目录中显示
```

#### 插入目录

```
\maketitle
\tableofcontents

在\maketitle后面插入这个控制序列
```

#### 插入数学公式

需要导入的宏包

```
\usepackage{amsmath}
```

#### 数学模式

分为两种： 行内模式，行间模式

**行内模式：**  在正文中插入 ，使用 **$ ... $**.

**行间模式：**独立排列，单独成行，自动居中，使用  \【    .\】

如果需要对行间模式的公式进行编号，使用 

```
\begin{equation}
\end{equation}
```



🍦🌼    接下来的部分将省略导言区的文本设置    🍦🌼



#### 上下标

```
\documentclass{artical}
\usepackage{amsmath}
\begin{document}
Einstein 's $E=mc^2$.

\[ E=mc^2. \]

\begin{equation}--------->可以进行编号的equation
E=mc^2.
\end{equation}----------->

\end{document}
```

**🎃******标点的要求****：

行内公式的标点，应该放在数学模式的限定符之外  **$E=mc^2$.**

行间公式则应该放在数学模式限定符之内  \ **\[ E=mc^2. \\]**

```
上标，用 ^ 实现
下标，用 _ 实现

```

默认只作用于**后面的一个字符**

如果想要对连续的几个字符起作用，要用 **{ }** 括起来

#### 根式和分式

- **根式用 ： \sqrt{ }**
- **分式用：\frac{ }{ }**,第一个参数为分子，第二个为分母

```
实践
\begin{document}
$\sqrt{x}$,$\frac{1}{2}$

\[\sqrt{x},\]

\[\frac{1}{2},\]
\end{documnet}
```

🍦🌼：如果要强制行内模式的分式显示为行间模式的大小，可以使用 **\dfrac**,反之可以使用  **\tfrac**

写行内分式，可以考虑使用 **xfrac** 宏包中的 **sfrac**来写分式

#### 运算符🐸

##### **连加**公式：

\sum_{i=1}^n
$$
\sum_{i=1}^n
$$
用 **\limits** 来强制显示地指定是否压缩这些上下标

\sum\limits _{i=1}^n
$$
\sum\limits _{i=1}^n
$$
**\quad** 代表当前字体下一个汉字的空白距离
**\qquad** 代表当前字体下两个汉字的空白距离

##### **连乘**公式：

 \prod_{i=1}^n
$$
\prod_{i=1}^n
$$

##### **极限**公式: 

\lim_{x\to0} \frac{e^2\cdot\sin x}{1+\sin x}
$$
\lim_{x\to0} \frac{e^2\cdot\sin x}{1+\sin x}
$$
**\to**表示趋近的那个箭头

**\cdot**表示乘法

**\sin** 表示正弦函数

**\infty** 表示无穷

**\pi** 表示Π

##### **积分**公式：

\int_a^b x^2 dx
$$
\int_a^b x^2 dx
$$
**\int_a^b** 表示积分的那个区间

多重积分可以使用：

```
\iint \iiint \iiiint \idotsint
```

$$
\iint\quad \iiint\quad \iiiint\quad \idotsint
$$

\idotsint 的效果： 中间无限省略号（dots)

##### 定界符

各种括号 包括 ( ),   [ ]  ,   \{\\}  ,   \langle\rangle  

花括号 {  }  通常 用来**输入命令**和**环境的参数**，所以数学公式中他们要在前面 加 **\\**

```
\big, \Big, \bigg, \Bigg
```

以上放在括号前面调整大小

**\Biggl(     x  \Biggr)**,

 **\Biggl（**  表示左边的括号增大，**\Biggr)**表示右边的括号增大
$$
\Biggl(x\Biggr)
$$

- 注意{}使用需要在前面加\    \Biggl\\{       \\Biggr\\}
  $$
  \Biggl \{\biggl \{\Bigl \{\bigl \{\{x\}\bigr \}\Bigr \}\biggr \}\Biggr\}
  $$

  $$
  \Biggl\langle\biggl\langle\Bigl\langle\bigl\langle\langle x
  \rangle\bigr\rangle\Bigr\rangle\biggr\rangle\Biggr\rangle
  
  \quad
  
  \Biggl\lvert\biggl\lvert\Bigl\lvert\bigl\lvert\lvert x
  \rvert\bigr\rvert\Bigr\rvert\biggr\rvert\Biggr\rvert
  
  \quad
  
   \Biggl\lVert\biggl\lVert\Bigl\lVert\bigl\lVert\lVert x
  \rVert\bigr\rVert\Bigr\rVert\biggr\rVert\Biggr\rVert省略号
  $$

  

##### 省略号

x_1,x_2,**\dots** ,x_n\quad 1,2,**\cdots** ,n\quad  **\vdots**\quad **\ddots**
$$
x_1,x_2,\dots ,x_n\quad 1,2,\cdots ,n\quad
\vdots\quad \ddots
$$
🐽**\dots** 和 **\cdots** 的纵向位置不同，前者一般用于有下表的序列

##### 矩阵

 `pmatrix`, `bmatrix`, `Bmatrix`, `vmatrix`, `Vmatrix`可以在矩阵两边加上各种分隔符

**语法**：  **\begin**{pmatrix}  a**&**b\\\c**&**d      **\end**{pmatrix}

begin和end表明，这是一个**环境**
$$
\begin{pmatrix} a&b\\c&d \end{pmatrix} \quad
\begin{bmatrix} a&b\\c&d \end{bmatrix} \quad
\begin{Bmatrix} a&b\\c&d \end{Bmatrix} \quad
\begin{vmatrix} a&b\\c&d \end{vmatrix} \quad
\begin{Vmatrix} a&b\\c&d \end{Vmatrix}
$$

##### 多行公式

- 手动换行
- 有些分段函数，需要加上左边的花括号

##### 长公式

- **不对齐**

​      使用 **`multline`** 环境

\\\实现换行，{ }实现留空
$$
\begin{multline}
x = a+b+c+{}\\
d+e+f+g
\end{multline}
$$

- **对齐**

使用 `aligned` j环境

此处 **{ }** 和 **& **起主要作用

&相当于制表符，对“对齐位置”进行定位，如果不加入&，默认右对齐
$$
\begin{aligned}
x ={}& a+b+c+{}\\
&d+e+f+g
\end{aligned}
$$

##### 公式组

无需对齐的公式组可以使用`gather` 环境

需要对齐的公式可以使用`align`环境，他们都带有**编号**如果**不需要编号**可以使用带星花的版本

（？这里没显示编号）
$$
\begin{gather}
a = b+c+d \\
x = y+z
\end{gather}
$$

$$
\begin{align}
a &= b+c+d \\
x &= y+z
\end{align}
$$

##### 分段函数

使用  `cases`  环境环境来实现，它必须包含在数学环境之内
$$
y= \begin{cases}
-x,\quad x\leq 0 \\
x,\quad x>0
\end{cases}
$$
**\leq** 表示 <= 符号

### 辅助工具



### 🧸知识点总结

1. 一个框架

   ```
   \documentclass{artical}
   \usingpackage{宏包amsmath}
   \title{}
   \author{}
   \date{}
   ..........
   \begin{document}
   \maketitle
   \tableofcontents
   \section{}
    \subsection{}
     \subsubsection{}
      \paragraph
       \subparagraph
   \end{document}
   ```

2. 公式框架

   ```
   $   $.
   $   $,$   $
   \[    .\]
   \begin{equation}
   
   \[    .\]
   
   \end{equation}
   ```

3. 符号

   
