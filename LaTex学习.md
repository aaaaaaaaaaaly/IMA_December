# LaTex学习

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

**行内模式：**  在正文中插入 ，使用 **$ ... $**

**行间模式：**独立排列，单独成行，自动居中，使用  \【...\】

如果需要对行间模式的公式进行编号，使用 

```
\begin{equation}
\end{equation}
```

#### 问题

实际在线编译的时候和平台没办法识别宏包
