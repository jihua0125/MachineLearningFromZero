### 数据科学的工具包
*“工欲善其事，必先利其器”*。

前面所讲是理论上的内容，那么在实践中该使用什么工具进行数据分析或者进行建模呢？这里介绍两门语言分别是`R`和`Python`。
`R`是一门面向统计学家的编程语言，最大的特点就是上手简单，对新手比较友好，对各类统计工具支持良好。当然它的缺点也比较明显，作为一门编程语言，`R`不够灵活，通用性较差，执行速度也很慢。`Python`则是一门通用语言，是目前除了`JavaScript`之外`GitHub`上[最流行的语言](http://www.businessinsider.com/the-9-most-popular-programming-languages-according-to-the-facebook-for-programmers-2017-10/#1-javascript-15)。它的优点是泛用性高，因为很多标准库和扩展包使用`C`进行编译，性能相对`R`而言有极大的提高（使用`R`处理百万量级的数据绝对会是噩梦）。另外不得不提`scikit-learn`包，[这个包](http://scikit-learn.org/stable/)可以被称之为 *机器学习的瑞士军刀*，几乎任何模型都可以在其中找到对应的支持，`Python`在数据科学领域的流行应该很大一部分也归功于它。如果你对上述两门语言没有任何偏好的话，我建议使用`R`做前期的数据清理工作，其中`tidyR`和`dplyR`两个包对表格结构数据支持非常好，可以实现类似`SQL`式的查询指令。另外`R`的`ggplot2`包在进行数据可视化方面也非常友好。在得到合适的数据格式之后，`Python`可以作为建立模型、训练、验证及测试的主要工具。接下来的内容将会介绍如何在`Windows 10`系统环境下安装`R`和`Python`。

除去这两门语言外，还有一些工具也需要提及一下。如果你是`Windows`用户，`Notepad++`是一个非常好用的文本编辑工具。如果你需要大量使用`csv`文件或者做文本相关数据处理，可以使用`Notepad++`进行处理。它对正则表达式支持非常好，可以使用一些简单的替换命令实现很多行`Python`代码才能实现的功能。如果你需要和别人合作，`Git`是一个很好的版本控制工具。

### 安装Python

本部分是给完全没有接触过`Python`及`Jupyter Notebook`的新人提供教学的，如果你已经了解以上内容，可以跳过此部分。

在数据科学中应用`Python`进行编程, 我的建议是使用`Anaconda`集成环境。`Anaconda`是一个专注于数据科学的`Python`平台，囊括了几乎全部常用的数据科学相关的包。其`Windows`版本下载地址为(https://www.anaconda.com/download/#windows)。另外，`Anaconda`集成了`Jupyter Notebook`， 这是一个非常好用的`Python`学习和交互式编程的工具。

*注意*，`Python`目前分为两个版本，`2.X`和`3.X` （X为次级版本号），目前`Python 2`最新版本为`2.7`, `Python 3`最新稳定版本为`3.6`。鉴于`Python 3`提供了很多新特性，因此在这里建议大家使用`Python 3.6`版本（本教程将会使用`Python 3.6`， 如果你使用别人的代码的话，请确定是`2.X`版本还是`3.X`版本，否则可能会出现 **执行错误**）。

#### 安装Anaconda
1. 进入上文所提供的下载地址（英文），按照`Windows`系统选择合适的版本，这里选择64位下载；
*提示*： 如果你不清楚你的操作系统是`32位`还是`64位`，可以右击 *开始* 按钮, 选择 *系统* ，在弹出的窗口中找到 *系统类型*。

2. 下载后，打开安装文件，按照提示操作；

3. 安装完成后，打开`cmd`(命令提示符)，输入`python`并按下`Enter`(回车键）。如果正确安装，你将会看到如下显示：
  `Python 3.6.3 |Anaconda custom (64-bit)| (default, Oct 15 2017, 03:27:45) [MSC v.1900 64 bit (AMD64)] on win32`
  `Type "help", "copyright", "credits" or "license" for more information.`
  `>>>`

4. 你可以键入`print("hello world")`，开始你的`python`编程之旅吧。

#### 使用Jupyter Notebook

1. 在`cmd`中输入命令`jupyter notebook`, 如果命令正确执行，你将会在浏览器中看到
<img src="https://i3vj1w-bn1305.files.1drv.com/y4mK6b8YeA3dNs3dVM93-tqbfGKbaejgzcfjVpi11gUTggkuWHOctSuO5dkNyYWRufiCVATLAVN9hjVkMe-fXYnG751ly-LRm9mHePkb568Cr-R-1wu2tEpijYPcuyjaOGAH4HQhu7e7YExYarHKjLWcN_80Gv_SnbYBXTFSEpgwMwb-CV5TuLjlG-vCdfb80LSUX9I_lNsFCYrzk2ITKCH8A?width=410&height=519&cropmode=none" width="410" height="519" />

2. 新建一个笔记本(`Notebook`): 点击右上角的`new`按钮，在下拉菜单中选择`Python 3`，这样就新建了一个基于`Python 3`内核的笔记本， 其中内核是指使用`Python 3`作为解释器。

3. 在新建的笔记本的第一个单元（`cell`）中输入`print("hello world")`， 并按下`Shift + Enter`组合键执行, 如果正确执行，你将会看到如下图所示结果：
<img src="https://zqk5dw-bn1305.files.1drv.com/y4mDKqPFY8PSnjCNqnqkzAgoe9zH_UALOE6nWsE5wdB43qnCTAoD1mfY2pRTz3DzIhRaIduAe2Kh3RYDtzxOWqLl5pvHvu7gr_jYsNC0D_keGEXyvJlsnA7_7OBR8a1cNk88TwTK3eL6niIAvxcba2cvaoDajT5aeIodKktBtf0kVKSCjPuxjpBA1Gu0Ps2vCVJ88lMpnSbgD-v-2VzG8qriQ?width=813&height=294&cropmode=none" width="813" height="294" />

*提示*： 单元格内为执行的代码，单元格下方为输出结果，单元格左侧[]内数字表示执行顺序，如果该单元格尚未执行，则[]为空。

`Shift + Enter`为执行当前单元格并将光标移动到下一单元格；`Ctrl + Enter`为执行当前单元格，并不会转移光标。
