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

（？这里没显示编号💧）
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

使用  `cases`  环境来实现，它必须包含在数学环境之内
$$
y= \begin{cases}
-x,\quad x< 0 \\
x,\quad x>0\\
0,\quad x=0
\end{cases}
$$
**\leq** 表示 <= 符号

#### 插入图片和表格

##### 图片

推荐使用 `usepackage{graphicx}`宏包提供的`\includegraphics`

```
\includegraphics[width=.8\textwidth]{a.jpg}
```

这样图片的宽度会被缩放到页面宽度的80%,

##### 表格

`tabular`环境提供简单的表格功能

`hline`命令表示横线

`|`命令表示竖线

`&`表示分列

`\\`表示换行

`l`,`c`,`r`分别表示每一列的居左，居中，居右

```
\begin{tabular}{|l|c|r|}   ................>环境配置，列数设置
 \hline                    ................>第一行，&用来分列
操作系统& 发行版& 编辑器\\
 \hline
Windows & MikTeX & TexMakerX \\
 \hline
Unix/Linux & teTeX & Kile \\
 \hline
Mac OS & MacTeX & TeXShop \\
 \hline
通用& TeX Live & TeXworks \\
 \hline
\end{tabular}
```

##### 浮动体

插图和表格通常需要占据很大的空间，经常需要调整他们的位置。

`figure`和`table`可以自动完成这样的任务，这种自动调整位置的环境称作 **float**

>```
>\begin{figure}[htbp]
>\centering
>\includegraphics{a.jpg}
>\caption{有图有真相}
>\label{fig:myphoto}
>\end{figure}
>```

> htbp:**here**,**top**,**bottom**,**float page** （这里，页顶，页底，浮动页）

`\centering`表示插图居中

`\caption`表示设置插图标题

`\label` 需要放在标题命令之后

#### 版面设置

**tips**:carousel_horse:在实际运用的时候需要自己去网络查文档，下面都是概念理解和宏包推荐

##### 页边距

设置页眉页脚，推荐使用`fancyhdr`宏包

:heavy_heart_exclamation:鉴于作者的推荐文档都是英文，这里把作者的示例copy做使用参考

```
可以在导言区加上如下几行：
\usepackage{fancyhdr}
\pagestyle{fancy}
\lhead{\author}页眉左边写上我的名字
\chead{\date}中间写上今天的日期
\rhead{152xxxxxxxx}右边写上我的电话
\lfoot{}
\cfoot{\thepage}页脚的正中写上页码
\rfoot{}
\renewcommand{\headrulewidth}{0.4pt}页眉和正文之间有一道宽为 0.4pt 的横线分割
\renewcommand{\headwidth}{\textwidth}
\renewcommand{\footrulewidth}{0pt}
```

##### 首行缩进

CTeX宏集解决了首行缩进的问题（即作者推荐的宏包）

##### 行间距

`setspace`宏包提供的命令来调整行间距

```
注意：行距是字号的1.5倍 和 1.5倍行距 不一样

\usepackage{setspace}
\onehalfspacing
在导言这样设置可以将行距设置为字号的1.5倍
```

##### 段间距

我们可以通过修改长度 `\parskip` 的值来调整段间距

```
\addtolength{\parskip}{.4em}

表示在原有基础上，增加段间距 0.4em ，如果要缩小距离，只需要将数值改为负值
```

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

   ```
   环境都会有 \begin{}
             \end{}
   上下标使用： ^ _
   根式使用： \sqrt{}
   分式使用:  \frac{}{}
   连加：\sum
   连乘：\prod
   极限：\lim
   积分：\int
   多重积分：\iint,\iiint,\iiiint
   上下标的压缩：\limits,\nolimits
   {}:通常用来 输入命令和环境的参数
   调整括号的大小：\big,\Big,\bigg,\Bigg
   省略号：\dots用于有序号下标的数列的省略
          \cdots用于没有序号下标的数列的省略
          \vdots
          \ddots
   矩阵-环境
   多行公式： 手动换行；//;分段函数使用cases环境
   不对齐： multline环境（不想要编号，加*）
   对齐：aligned环境
   公式组：无需对齐gather环境，对齐align环境
   \quad是空格
   \to表示趋近的那个箭头
   \cdot表示乘法
   \sin表示正弦函数
   \infty 表示无穷
   \pi 表示Π
   ```
   
   :herb:初步入门达成！有了概念性理解
   
   不过实际运用过程中需要去查正式的文档，已经将作者的归档文件下载：LaTeX——Docs，可以参考本地下载文件
