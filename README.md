Bokeh是一个很美观实用的Python交互绘图库，但是他的官方文档并不十分好查阅，加上现在还没有中文文档，所以我打算将其用户指南翻译出来，也方便更多人学习。

这个项目预计一个月完成，之后申请官方认证。

由于是第一次组织这种活动，经验不足，还望多指正。

### 一些小说明

- 若想成为Collaborator请提交Issue或E-mail我，内容包括：你的ID，每天用于翻译的时间


- 非Collaborator请push README.md中的相关问题，不要push其他目录中的问题


- 由于Markdown不能显示HTML，交互式图形暂时以截图的方式展示
- 更新周期为1天，每天晚上0点我会把一天的提交整合到README.md，方便大家阅读

### Collaborator注意事项

- 所有标题加上英文版标题

  如 快速入门（Quickstart）


- 大标题以二级标题（**两个#**）显示，如

  ## 快速入门（Quickstart）

- 要翻译哪一部分请提前Issue或者E-mail我，先来后到哦~

- push的Markdown文档统一保存在`/tmp`路径下，命名格式为

  大标题(你的ID)  ------------------**括号为中文括号**

  如 我翻译快速入门（Quickstart）可以保存为

  **快速入门（DonaldDai）.md**

  `/tmp`中的文档我每天晚上0点会整合一次

- 交互式图形截图统一保存在`/img`路径下，命名规则为 

  大标题选择简写\[-下一级标题选择简写\[顺序编号\]\]

  如 在Qickstart-Linked panning and brushing下的两张图片可以保存为

  **QickStart-LinkedPanningandBrushing1.png**和**QickStart-LinkedPanningandBrushing2.png**

  或者

  **QS-LPB1.png**和**QS-LPB2.png**

- 参与者push的时间务必在**11：30**之前

  pull到本地的时间最好在**12：00**之后

- 每次push请添加清晰的说明

  比如 push的大概内容、更新了哪个名词的单词或者是通俗化了一些句子等

  养成良好的说明习惯也方便日后自己查阅

- 如果你喜欢记得给Star哦 : ) 本人急需Star撑场

###待处理问题

例子结果能不显示在Makedown中，是否要链接到外网上？

# Bokeh中文用户指南

目录

- User Guide
- [快速入门（Quickstart）](#快速入门（Quickstart）)
- Getting Set Up
- Defining Key Concepts
- Plotting with Basic Glyphs
- Making High-level Charts
- Leveraging Other Libraries
- Adding Annotations
- Styling Visual Attributes
- Configuring Plot Tools
- Laying out Plots and Widgets
- Working in the Notebook
- Adding Interactions
- Linking Plots
- Adding Widgets
- JavaScript Callbacks
- Using Bokeh Commands
- Running a Bokeh Server
- Embedding Plots and Apps
- Speeding up with WebGL
- Mapping Geo Data
- Developing with JavaScript
- Extending Bokeh
- Learning More
- Tutorials

## 快速入门(Quickstart)

原文 [Quickstart](http://bokeh.pydata.org/en/latest/docs/user_guide/quickstart.html)

### 介绍（Introduction）

Bokeh是致力于网页浏览器展示的Python交互式图表库。Bokeh能读取巨大的数据集或者流数据以简单快捷的方式为网页提供优美、简洁、高交互性能的图形。

为了能让用户高度自定义简单、高性能、灵活的图表，Bokeh开放三个层次的接口给用户：

- [`bokeh.models`](http://bokeh.pydata.org/en/latest/docs/reference/models.html#bokeh-models)   低级接口，能为app开发者提供高度灵活的图形表示（可以自定义一些顶层的组件）
- [`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)  中级接口，该接口主要用于绘制曲线（默认加载一些低级的组件）
- [`bokeh.charts`](http://bokeh.pydata.org/en/latest/docs/reference/charts.html#bokeh-charts) 高级接口，能快速简单地构建复杂的图形

快速入门只能主要运用 [bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口

### 快速安装

Bokeh有多种安装方式，Bokeh推荐在 [Anaconda Python distribution](http://continuum.io/anaconda)的命令窗口来安装，这是最简单的方法。

```
conda install bokeh
```

该命令会安装Bokeh所有的依赖包。

Anaconda最小安装适用于包括Windows等大多数系统，在安装的同时也会在Anaconda的根目录中创建一个`examples/`的子目录，其中包含了一些例子。

如果你已经安装了Bokeh所有的依赖包，比如Numpy，那么你也可以通过`pip`来安装：

```
pip install bokeh
```

> 注意
>
> pip安装方式不安装示例。若要查看示例可以`Clone`下Git仓库中的`examples/`到本地。[HELP此处应有超链接]

### 开始

Bokeh是一个很大的库，功能丰富，而这一章节中只是对Bokeh常用的示例和工作流进行简单讲解。若要了解更多功能，请参见 [User Guide](http://bokeh.pydata.org/en/latest/docs/user_guide.html#userguide)

下面是一些示例

以Python列表（List）作为参数传入绘制带交互工具（缩放、画笔、自适应大小、保存等）的图

```python
from bokeh.plotting import figure, output_file, show

# prepare some data
x = [1, 2, 3, 4, 5]
y = [6, 7, 2, 4, 5]

# output to static HTML file
output_file("lines.html")

# create a new plot with a title and axis labels
p = figure(title="simple line example", x_axis_label='x', y_axis_label='y')

# add a line renderer with legend and line thickness
p.line(x, y, legend="Temp.", line_width=2)

# show the results
show(p)
```

![](/img/QS-GS1.png)

当运行这段代码之后，会在项目当前目录下创建一个`"lines.html"`文件，并且浏览器会自动打开一个新标签页来显示刚刚创建的图表（为展示需要，会把代码生成的图形放在此文档中，以供参考）

用 [`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口创建图表的基本步骤如下：

- 准备一些数据（在上面的例子中，数据是一个简单的Python列表）
- 指定一个输出（在上面的例子中，用`output_file()`函数指定了输出文件名为`"lines.html"`）
- 调用`figure()`函数创建图表容器并指定一些整体参数，比如title、tools和axes labels
- 将数据传入渲染函数（在上面的例子中是`Figure.line`函数）并指定一些视觉参数，比如colors、legends和widths
- 调用`show()`或者`save()`来显示或保存结果

步骤三、四可以重复使用来绘制多个图形，多图形绘制可以参考在下面的例子

若要用 [bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting) 自定义添加更多数据、曲线或对数轴非常方便简洁的，比如在一个图形中同时绘制多条曲线的代码如下：

```python
from bokeh.plotting import figure, output_file, show

# prepare some data
x = [0.1, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0]
y0 = [i**2 for i in x]
y1 = [10**i for i in x]
y2 = [10**(i**2) for i in x]

# output to static HTML file
output_file("log_lines.html")

# create a new plot
p = figure(
   tools="pan,box_zoom,reset,save",
   y_axis_type="log", y_range=[0.001, 10**11], title="log axis example",
   x_axis_label='sections', y_axis_label='particles'
)

# add some renderers
p.line(x, x, legend="y=x")
p.circle(x, x, legend="y=x", fill_color="white", size=8)
p.line(x, y0, legend="y=x^2", line_width=3)
p.line(x, y1, legend="y=10^x", line_color="red")
p.circle(x, y1, legend="y=10^x", fill_color="red", line_color="red", size=6)
p.line(x, y2, legend="y=10^x^2", line_color="orange", line_dash="4 4")

# show the results
show(p)
```

![](/img/QS-GS2.png)

### 在Jupyter Notebooks上运用Bokeh

在这一小节中，我们将会讲解Jypyter Notebooks上Bokeh的使用

Jupyter Notebooks是一款风靡于“PyData”社区的强大的数据分析工具。Bokeh无缝整合了Jupyter Notebooks和Bokeh。如果想在Notebook中查看之前的示例，只需要将`output_file()`替换成`output_notebook()`即可。

在 [Bokeh NBViewer Gallery](http://nbviewer.ipython.org/github/bokeh/bokeh-notebooks/blob/master/index.ipynb)还有许多静态示例，有兴趣的可以去看看。

在 [Bokeh GitHub repository](https://github.com/bokeh/bokeh)上也有大量的notebook示例，若想要查看，可以`clone`下整个仓库，之后再命令行中进入其中的`example/howto`子目录，接着运行

```
ipython notebook
```

你可以在自动弹出的索引页直接打开其中的文件或者执行任何其他交互操作。特别是你可以从以下两个例子中体会到Bokeh是如何与Jupyter挂件协同工作的。

[examples/howto/notebook_comms/Jupyter Interactors.ipynb](https://github.com/bokeh/bokeh/tree/0.12.1/examples/howto/notebook_comms/Jupyter%20Interactors.ipynb)

[examples/howto/notebook_comms/Numba Image Example.ipynb](https://github.com/bokeh/bokeh/tree/0.12.1/examples/howto/notebook_comms/Numba%20Image%20Example.ipynb)

### 其他语言版本的Bokeh

Bokeh的体系结构使得Bokeh能够非常容易的为其他语言提供使用接口，其中有一些小众语言的接口已经存在（比如R，Scala，Julia）。尽管我们团队是Python的忠实粉丝，但是我们也同时在开发着不同语言的Bokeh库，可以通过以下链接查看已经编译完的一些多语言Bokeh库

- [Bokeh for R](http://hafen.github.io/rbokeh/)
- [Bokeh for Scala](https://github.com/bokeh/bokeh-scala)
- [Bokeh for Julia](https://github.com/bokeh/Bokeh.jl)

### 示例数据

示例中所用的数据和示例是分开存放的，若要下载这些数据，可以在Bash或者Windows命令提示符后键入命令

```
bokeh sampledata
```

### 相关概念

根据上面的一些例子，这里提出一些核心概念

#### 图形（Plot）

图形是Bokeh的中心概念。图形在Bokeh中指的是容纳曲线、指示、数据、工具等几乎所有用来展示的元素的一个容器。具体的，Bokeh中的 [`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口提供了一个 `Figure`类来聚集所有这些必要的元素，而`Fighure`实例可以很方便的由`figure()`函数来创建

#### 标示（Glyphs）

标示是Bokeh中的基础视觉元素。在Bokeh的底层，标示以**glyph对象**存在，比如`Line`。如果你要使用低级接口[`bokeh.models`](http://bokeh.pydata.org/en/latest/docs/reference/models.html#bokeh-models)来绘制图形，那么你还需要创建所有必要的Bokeh对象，其中包括上面提到的glyph对象和对应的数据集。为了使用更方便，[`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)提供一个更高级的**glyph方法**像本章第一个示例中用的`Figure.line`就是其中一个。第二个示例中增加了`Figure.circle`来同时显示曲线和圆。除了曲线和圆，Bokeh还有许多可选的[标示](http://bokeh.pydata.org/en/latest/docs/reference/models/glyphs.html#bokeh-models-glyphs)和[标志](http://bokeh.pydata.org/en/latest/docs/reference/models/markers.html#bokeh-models-markers)。

视觉元素的外观和数据的值是紧密相关的。在上面的例子中，我们可以看到*x*和*y*参数是可以被赋值为向量的。但其实标示还有许多可选的属性参数，如[线形属性](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling-line-properties)、[填充属性](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling-fill-properties)和[文字属性](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling-text-properties)。所有这些参数都可以以向量的形式赋值给参数，在下面会给出相关示例

#### 指示&说明（Guides and Annotations）

Bokeh还提供一些别的视觉组件才帮助用户更好的展示或者让用户在图中做比较。这一类组件分为两类

- 指示（Guides）：指示的作用主要是帮助用户判断图中的距离，角度等。具体的包括格线、坐标轴等
- 说明（Annotations）：说明主要包括图中的标签部分，具体的比如有标题，图例等

#### 数据范围（Ranges）

数据范围指的是绘图过程中所使用的数据的上界与下界。默认情况下，用[`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口绘制出的图像时，Bokeh的`DataRangeld`对象会根据所用数据计算出数据范围，之后传给绘图函数。当然，数据范围也可以手动传入，只需要在绘图时传入如下参数，参数可以接受Python中的列表或者二元元组形式的赋值

```python
p = figure(x_range=[0,10], y_range=(10, 20))
```

#### 相关资源（Resources）

若要在用户本地展示图形，要求所使用的浏览器加载Bokeh的JS和CSS文件。默认情况下，`output_file()`函数会自动在生成的HTML中加载来自 [http://cdn.pydata.org](http://cdn.pydata.org/) 的样式文件。但是，你也可以将文件下载下来，之后再本地载入，若要使用这种方式请在`output_file()`函数中添加参数`mode="inline"`。

### 更多例子

下面给出更多在别的场合下经常会用到的例子，所有这些例子都是用[`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口绘制的。

#### 以向量形式传入颜色和尺寸

这个例子主要演示如何传入一系列的数据给绘图参数如`fill_color`和`radius`。你也可以在这个例子中找到以下方式的用法：

- 传入一个包含工具名称的列表给`figure()`
- 用`mode`参数从CDN获取BokehJS文件
- 自定义`x_range`和`y_range`参数
- 传入空值`None`来*擦掉*一条曲线
- 运用Numpy数组来传入数据

```python
import numpy as np

from bokeh.plotting import figure, output_file, show

# prepare some data
N = 4000
x = np.random.random(size=N) * 100
y = np.random.random(size=N) * 100
radii = np.random.random(size=N) * 1.5
colors = [
    "#%02x%02x%02x" % (int(r), int(g), 150) for r, g in zip(50+2*x, 30+2*y)
]

# output to static HTML file (with CDN resources)
output_file("color_scatter.html", title="color_scatter.py example", mode="cdn")

TOOLS="resize,crosshair,pan,wheel_zoom,box_zoom,reset,box_select,lasso_select"

# create a new plot with the tools above, and explicit ranges
p = figure(tools=TOOLS, x_range=(0,100), y_range=(0,100))

# add a circle renderer with vectorized colors and sizes
p.circle(x,y, radius=radii, fill_color=colors, fill_alpha=0.6, line_color=None)

# show the results
show(p)
```

[HELP Picture]

[To be continue].
