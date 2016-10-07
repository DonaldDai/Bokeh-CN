Bokeh是一个很美观实用的Python交互绘图库，但是他的官方文档并不十分好查阅，加上现在还没有中文文档，所以我打算将其用户指南翻译出来，也方便更多人学习。

这个项目预计一个月完成，之后申请官方认证。

由于是第一次组织这种活动，经验不足，还望多指正。

### 一些小说明

- 若想成为Collaborator请提交Issue或E-mail我，内容包括：你的ID，每天用于翻译的时间


- 非Collaborator请push README.md中的相关问题，不要push其他目录中的问题


- 由于Markdown不能显示HTML，交互式图形暂时以截图的方式展示
- 更新周期为1天，每天晚上0点我会把一天的提交整合到README.md，方便大家阅读

### 参与注意选项

请移步[CONTRIBUTING](./CONTRIBUTING.md)

###待处理问题

文章结构怎么更美观...

# Bokeh中文用户指南

目录

- <a href="#UserGuide">用户指南-User Guide</a>
- <a href="#Quickstart">快速入门-Quickstart</a>
- <a href="#GettingSetUp">设置-Getting Set Up</a>
- <a href="#DefiningKeyConcepts">一些重要概念-Defining Key Concepts</a>
- <a href="#PlottingwithBasicGlyphs">用基础标志绘图-Plotting with Basic Glyphs</a>
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
- <a href="#EmbeddingPlotsandApps">嵌入图表和Apps-Embedding Plots and Apps</a>
- Speeding up with WebGL
- Mapping Geo Data
- Developing with JavaScript
- Extending Bokeh
- Learning More
- Tutorials

## <p id="UserGuide">用户指南（User Guide）</p>

这一章内容主要是了解一下整片用户指南的大体结构，根据你可能用到的情况，你可以挑选不同的章节去了解。章节根据内容分为：

### 快速入门-Quickstart

主要是走马观花的带你过一遍基本的功能和用法。

### 设置-Getting Set Up

验证你的Bokeh是否安装成功

### 插入图表或Apps-Embedding Plots and Apps

以多种方式在HTML文档中嵌入静态或基于Bokeh服务器的交互图表

### 一些重要概念-Defining Key Concepts

定义和解释一些基本的概念

## <p id="Quickstart">快速入门-Quickstart</p>

原文 [Quickstart](http://bokeh.pydata.org/en/latest/docs/user_guide/quickstart.html)

### 介绍-Introduction

Bokeh是致力于网页浏览器展示的Python交互式图表库。Bokeh能读取巨大的数据集或者流数据以简单快捷的方式为网页提供优美、简洁、高交互性能的图形。

为了能让用户高度自定义简单、高性能、灵活的图表，Bokeh开放三个层次的接口给用户：

- [`bokeh.models`](http://bokeh.pydata.org/en/latest/docs/reference/models.html#bokeh-models)   低级接口，能为app开发者提供高度灵活的图形表示（可以自定义一些顶层的组件）
- [`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)  中级接口，该接口主要用于绘制曲线（默认加载一些低级的组件）
- [`bokeh.charts`](http://bokeh.pydata.org/en/latest/docs/reference/charts.html#bokeh-charts) 高级接口，能快速简单地构建复杂的图形

快速入门只能主要运用 [bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口

### 快速安装-Quick Installation

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

### 开始-Getting Started

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

![](/img/QS_GS1.png)

[交互图](/jupyter/QS_GS1.ipynb)

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

![](/img/QS_GS2.png)

[交互图](/jupyter/QS_GS2.ipynb)

### Jupyter Notebooks上的应用-Jupyter Notebooks

在这一小节中，我们将会讲解Jypyter Notebooks上Bokeh的使用

Jupyter Notebooks是一款风靡于“PyData”社区的强大的数据分析工具。Bokeh无缝整合了Jupyter Notebooks和Bokeh。如果想在Notebook中查看之前的示例，只需要将`output_file()`替换成`output_notebook()`即可，注意这里`output_notebook()`不需要参数。

在 [Bokeh NBViewer Gallery](http://nbviewer.ipython.org/github/bokeh/bokeh-notebooks/blob/master/index.ipynb)还有许多静态示例，有兴趣的可以去看看。

在 [Bokeh GitHub repository](https://github.com/bokeh/bokeh)上也有大量的notebook示例，若想要查看，可以`clone`下整个仓库，之后再命令行中进入其中的`examples/howto`子目录，接着运行

```
ipython notebook
```

你可以在自动弹出的索引页直接打开其中的文件或者执行任何其他交互操作。特别是你可以从以下两个例子中体会到Bokeh是如何与Jupyter挂件协同工作的。

[examples/howto/notebook_comms/Jupyter Interactors.ipynb](https://github.com/bokeh/bokeh/tree/0.12.1/examples/howto/notebook_comms/Jupyter%20Interactors.ipynb)

[examples/howto/notebook_comms/Numba Image Example.ipynb](https://github.com/bokeh/bokeh/tree/0.12.1/examples/howto/notebook_comms/Numba%20Image%20Example.ipynb)

### 多语言支持-Other Languages

Bokeh的体系结构使得Bokeh能够非常容易的为其他语言提供使用接口，其中有一些小众语言的接口已经存在（比如R，Scala，Julia）。尽管我们团队是Python的忠实粉丝，但是我们也同时在开发着不同语言的Bokeh库，可以通过以下链接查看已经编译完的一些多语言Bokeh库

- [Bokeh for R](http://hafen.github.io/rbokeh/)
- [Bokeh for Scala](https://github.com/bokeh/bokeh-scala)
- [Bokeh for Julia](https://github.com/bokeh/Bokeh.jl)

### 示例数据-Sample Data

示例中所用的数据和示例是分开存放的，若要下载这些数据，可以在Bash或者Windows命令提示符后键入命令

```
bokeh sampledata
```

### 相关概念-Concepts

根据上面的一些例子，这里提出一些核心概念

#### 图形-Plot

图形是Bokeh的中心概念。图形在Bokeh中指的是容纳曲线、指示、数据、工具等几乎所有用来展示的元素的一个容器。具体的，Bokeh中的 [`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口提供了一个 `Figure`类来聚集所有这些必要的元素，而`Fighure`实例可以很方便的由`figure()`函数来创建

#### 标示-Glyphs

标示是Bokeh中的基础视觉元素。在Bokeh的底层，标示以**glyph对象**存在，比如`Line`。如果你要使用低级接口[`bokeh.models`](http://bokeh.pydata.org/en/latest/docs/reference/models.html#bokeh-models)来绘制图形，那么你还需要创建所有必要的Bokeh对象，其中包括上面提到的glyph对象和对应的数据集。为了使用更方便，[`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)提供一个更高级的**glyph方法**像本章第一个示例中用的`Figure.line`就是其中一个。第二个示例中增加了`Figure.circle`来同时显示曲线和圆。除了曲线和圆，Bokeh还有许多可选的[标示](http://bokeh.pydata.org/en/latest/docs/reference/models/glyphs.html#bokeh-models-glyphs)和[标志](http://bokeh.pydata.org/en/latest/docs/reference/models/markers.html#bokeh-models-markers)。

视觉元素的外观和数据的值是紧密相关的。在上面的例子中，我们可以看到*x*和*y*参数是可以被赋值为向量的。但其实标示还有许多可选的属性参数，如[线形属性](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling-line-properties)、[填充属性](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling-fill-properties)和[文字属性](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling-text-properties)。所有这些参数都可以以向量的形式赋值给参数，在下面会给出相关示例

#### 指示&说明-Guides and Annotations

Bokeh还提供一些别的视觉组件才帮助用户更好的展示或者让用户在图中做比较。这一类组件分为两类

- 指示（Guides）：指示的作用主要是帮助用户判断图中的距离，角度等。具体的包括格线、坐标轴等
- 说明（Annotations）：说明主要包括图中的标签部分，具体的比如有标题，图例等

#### 数据范围-Ranges

数据范围指的是绘图过程中所使用的数据的上界与下界。默认情况下，用[`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口绘制出的图像时，Bokeh的`DataRangeld`对象会根据所用数据计算出数据范围，之后传给绘图函数。当然，数据范围也可以手动传入，只需要在绘图时传入如下参数，参数可以接受Python中的列表或者二元元组形式的赋值

```python
p = figure(x_range=[0,10], y_range=(10, 20))
```

#### 相关资源-Resources

若要在用户本地展示图形，要求所使用的浏览器加载Bokeh的JS和CSS文件。默认情况下，`output_file()`函数会自动在生成的HTML中加载来自 [http://cdn.pydata.org](http://cdn.pydata.org/) 的样式文件。但是，你也可以将文件下载下来，之后再本地载入，若要使用这种方式请在`output_file()`函数中添加参数`mode="inline"`。

### 更多例子-More examples

下面给出更多在别的场合下经常会用到的例子，所有这些例子都是用[`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口绘制的。

#### 参数向量化-Vectorized colors and sizes

这个例子主要演示如何传入一系列的数据给绘图参数如`fill_color`和`radius`。你也可以在这个例子中找到以下情况的用法：

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

![](/img/QS_ME_VCS.png)

[交互图](/jupyter/QS_ME_VCS.ipynb)

#### 数据联动-Linked panning and brushing

> 什么是数据联动？
>
> 在这个例子中，数据联动指的是一个图形中的数据变化会影响到另一个图形中的数据

有时候在不同的图形中添加联动的数据曲线更有利于战术数据。在Bokeh中进行数据联动，一般只需在几个图形间传递将组件参数即可。下面的例子演示了在Bokeh的笔工具联动**（linked panning）**，方法是在图形间传递几个组件参数。你也可以在下面的例子中找到一下情况的用法：

- 通过多次调用`figure()`函数来创建多个图形
- 用`gridplot()`函数来排列多个图形
- 用`Figure.triangle`和`Figure.square`在图形中添加新的标识
- 通过调节`toolbar_location`的值为`None`来隐藏工具栏
- `line_color`、`fill_color`、`line_alpha`、`fill_alpha`属性的用法

```python
import numpy as np

from bokeh.layouts import gridplot
from bokeh.plotting import figure, output_file, show

# prepare some data
N = 100
x = np.linspace(0, 4*np.pi, N)
y0 = np.sin(x)
y1 = np.cos(x)
y2 = np.sin(x) + np.cos(x)

# output to static HTML file
output_file("linked_panning.html")

# create a new plot
s1 = figure(width=250, plot_height=250, title=None)
s1.circle(x, y0, size=10, color="navy", alpha=0.5)

# NEW: create a new plot and share both ranges
s2 = figure(width=250, height=250, x_range=s1.x_range, y_range=s1.y_range, title=None)
s2.triangle(x, y1, size=10, color="firebrick", alpha=0.5)

# NEW: create a new plot and share only one range
s3 = figure(width=250, height=250, x_range=s1.x_range, title=None)
s3.square(x, y2, size=10, color="olive", alpha=0.5)

# NEW: put the subplots in a gridplot
p = gridplot([[s1, s2, s3]], toolbar_location=None)

# show the results
show(p)
```

![](/img/QS_ME_LPB1.png)

[交互图](/jupyter/QS_ME_LPB1.ipynb)

尽管工具栏是隐藏的，但是笔工具仍然处于激活状态。点击并拖动图形可以改变坐标轴的范围，同时你也可以观察到三个图形的坐标轴数据是怎么联动的

另一个例子是**选择联动（linked brushing）**， 实现的方式是在两个图形中传递[`ColumnDataSource`](http://bokeh.pydata.org/en/latest/docs/reference/models/sources.html#bokeh.models.sources.ColumnDataSource)数据结构参数。

```python
import numpy as np
from bokeh.plotting import *
from bokeh.models import ColumnDataSource

# prepare some date
N = 300
x = np.linspace(0, 4*np.pi, N)
y0 = np.sin(x)
y1 = np.cos(x)

# output to static HTML file
output_file("linked_brushing.html")

# NEW: create a column data source for the plots to share
source = ColumnDataSource(data=dict(x=x, y0=y0, y1=y1))

TOOLS = "pan,wheel_zoom,box_zoom,reset,save,box_select,lasso_select"

# create a new plot and add a renderer
left = figure(tools=TOOLS, width=350, height=350, title=None)
left.circle('x', 'y0', source=source)

# create another new plot and add a renderer
right = figure(tools=TOOLS, width=350, height=350, title=None)
right.circle('x', 'y1', source=source)

# put the subplots in a gridplot
p = gridplot([[left, right]])

# show the results
show(p)
```

![](/img/QS_ME_LPB2.png)

[交互图](/jupyter/QS_ME_LPB2.ipynb)

选择方形选择工具（box select）或者套索选择工具（lasso select）在其中一个图形中进行操作，这个操作会联动另一个图形。

#### 时间序列图形-Datetime axes

处理时间序列数据是数据分析中另一常见的情形。Bokeh有一个成熟的类 [`DatetimeAxis`](http://bokeh.pydata.org/en/latest/docs/reference/models/axes.html#bokeh.models.axes.DatetimeAxis)，可以根据现有的图形来生成时间序列图形。[`DatetimeAxis`](http://bokeh.pydata.org/en/latest/docs/reference/models/axes.html#bokeh.models.axes.DatetimeAxis)的一些坐标轴的参数有默认值，当然你也可以不用[`DatetimeAxis`](http://bokeh.pydata.org/en/latest/docs/reference/models/axes.html#bokeh.models.axes.DatetimeAxis)而看情况直接将`figure()`中`x_axis_type`或`y_axis_type`的值设为`"datetime"`来说明绘图的类型是时间序列。

这个例子中也有一些有趣的用法：

- 设置`figure()`函数中的`width`和`height`参数
- 通过改变参数自定义图形和其他对象
- 通过设置`figure`的参数（如`legend`、`grid`、`xgrid`、`ygrid`、`axis`、`xaxis`、`yaxis`）来调整图形中的注释

```python
import numpy as np

from bokeh.plotting import figure, output_file, show
from bokeh.sampledata.stocks import AAPL

# prepare some data
aapl = np.array(AAPL['adj_close'])
aapl_dates = np.array(AAPL['date'], dtype=np.datetime64)

window_size = 30
window = np.ones(window_size)/float(window_size)
aapl_avg = np.convolve(aapl, window, 'same')

# output to static HTML file
output_file("stocks.html", title="stocks.py example")

# create a new plot with a a datetime axis type
p = figure(width=800, height=350, x_axis_type="datetime")

# add renderers
p.circle(aapl_dates, aapl, size=4, color='darkgrey', alpha=0.2, legend='close')
p.line(aapl_dates, aapl_avg, color='navy', legend='avg')

# NEW: customize by setting attributes
p.title.text = "AAPL One-Month Average"
p.legend.location = "top_left"
p.grid.grid_line_alpha=0
p.xaxis.axis_label = 'Date'
p.yaxis.axis_label = 'Price'
p.ygrid.band_fill_color="olive"
p.ygrid.band_fill_alpha = 0.1

# show the results
show(p)
```

![](/img/QS_ME_DA.png)

[交互图](/jupyter/QS_ME_DA.ipynb)

> 注意
>
> 这里绘图需要下载一些官方资源，已经下载的上述代码运行不会出问题，如果上述代码运行出错请根据提示
>
> ```python
> from bokeh.sampledata import download
> download()
> ```
>
> 下载相关资源

### Bokeh图形服务器-Bokeh Plot Server

Bokeh服务器是一个可选的组件项。尽管没有Bokeh图形服务器，我们一样可以创建出有趣、可交互的可视化数据。但是Bokeh还有一些新颖、强大的能力或许你会想用到

- 用UI和选项来驱动图形的计算和更新
- 能够降低大型数据集采样率的智能服务端
- 通过流数据自动更新图形
- 适用于大数据的成熟图形重绘系统
- 发布更易于普通用户操作的可视化图形

由于空间有限，不能在快速入门中讲解所有的用法，读者可以现在下面这个例子中感受一些Bokeh图形服务器的强大。

![](/img/QS_BPS.png)

你可以在 [Gallery](http://bokeh.pydata.org/en/latest/docs/gallery.html#gallery)的 [Server App Examples](http://bokeh.pydata.org/en/latest/docs/gallery.html#gallery-server-examples)部分中找到更多有关图形服务器绘图的例子。想要知道更多图形服务器的细节请移步 [User Guide](http://bokeh.pydata.org/en/latest/docs/user_guide.html#userguide)的[Running a Bokeh Server](http://bokeh.pydata.org/en/latest/docs/user_guide/server.html#userguide-server)部分

### 下一步干啥？-What’s next?

【困了。睡觉。。。】

## <p id="GettingSetUp">设置-Getting Set Up</p>

这一章的第一部分会指引你快速安装一下Bokeh并做一些小测试来检测一下是否安装正常。

### 安装Bokeh库-Installing the Bokeh Library

安装Bokeh最简单的方法就是用诸如`pip`、`conda`等包管理工具来安装。如果你用过 [Anaconda](http://continuum.io/anaconda)那么你可以用`conda`来安装

```
conda install bokeh
```

否则，就用`pip`工具来安装

```
pip install bokeh
```

如果要查看更多安装方面的细节可以参考Bokeh文档的[安装](http://bokeh.pydata.org/en/latest/docs/installation.html#installation)部分。

### 验证安装-Verifying your installation

第一步你可以在Python的交互式命令行中`import bokeh`，用`bokeh.__version__`来查看当前安装的版本。如果你能成功执行命令，结果应该长这样：

![](/img/GSU_VYI1.png)

第二步，你可以用Bokeh绘制一个简单的图形来检测是否安装正常。将下面的代码保存到文件中并执行或者直接在Python交互式命令行中键入下面的代码来绘制一副简单的图形。

```python
from bokeh.plotting import figure, output_file, show
output_file("test.html")
p = figure()
p.line([1, 2, 3, 4, 5], [6, 7, 2, 4, 5], line_width=2)
show(p)
```

这段代码会生成一个名为`test.html`的本地文件，并且会自动打开默认浏览器来显示图形。正常运行的图形应该是这样的

![](/img/GSU_VYI2.png)

你也可以在IPython/Jupyter notebook中执行上述的代码来绘制图形，但是需要把上面代码中的`output_file`替换成`output_notebook`。结果如下

![](/img/GSU_VYI3.png)

### 寻求帮助？-Finding Help

如果在你安装或者运行示例的时候出现问题了，可以发Email到[Bokeh mailing list](https://groups.google.com/a/continuum.io/forum/#!forum/bokeh)寻求帮助，也可以在[Bokeh GitHub issue tracker](https://github.com/bokeh/bokeh/issues)中提交Issue。

## <p id="DefiningKeyConcepts">一些重要概念-Defining Key Concepts</p>

## 一些重要概念-Defining Key Concepts

### 术语表-Glossary

为了更好的使用用户指南，了解相关高级概念很重要。下面是一份小术语表，上面介绍了一些Bokeh的重要概念

------

**应用**

Bokeh应用指的是一个已经渲染过的文件，结果一般运行在浏览器中。

**BokehJS文件**

Bokeh的Javascript文件主要用于渲染图形和UI中的交互工具。一般用户不需要考虑JavaScript文件中的内容，但如果你知道一些关于JavaScript和Bokeh之间的联系的知识，那最好不过啦。更多细节可以查看[开发者指南](http://bokeh.pydata.org/en/latest/docs/dev_guide.html#devguide)中的[BokehJS](http://bokeh.pydata.org/en/latest/docs/dev_guide/bokehjs.html#devguide-bokehjs)。

**图表**

示例中的静态图如柱状图，水平延伸的图和时间序列图等都可以由Bokeh提供的`bokeh.charts`高级接口来快速构建。更多示例及用法请查看 [构建高级图表](http://bokeh.pydata.org/en/latest/docs/user_guide/charts.html#userguide-charts)。

**文件**

文件指的是Bokeh应用所使用的数据集。文件中包含Bokeh应用渲染图表和交互工具所要用到的所有模型和数据。

**嵌入**

嵌入指的是在Web应用、网页或者Jupyter（Ipython） Notebook中插入Bokeh的图标。更多细节请查看 [插入图表或Apps](http://bokeh.pydata.org/en/latest/docs/user_guide/embed.html#userguide-embed)。

**标志**

标志是构建Bokeh图形的基础元素，如曲线、三角形、方形、楔形、图示等都属于标志。`bokeh.plotting`接口提供了便捷的方法创建自定义标志。更多细节请查看 [Plotting with Basic Glyphs](http://bokeh.pydata.org/en/latest/docs/user_guide/plotting.html#userguide-plotting)。

**模型**

模型是Bokeh中最底层的类，模型的作用就是组成Bokeh应用的整个“轮廓（scenegraphs）”。这些类在`bokeh.models`接口里。大多数的用户不会直接接触到这些底层的类。然而最终的Bokeh应用是由这些类的集合组成的，所以理解它也是非常重要的，这样你可以更随心所欲的绘制Bokeh图形。更多信息请查看[Styling Visual Attributes](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling)。

**Bokeh服务器**

Bokeh服务器是一个可选项，即使不使用Bokeh可以在浏览器中渲染交互图形。Bokeh服务器主要用于发布或分享交流Bokeh图形或者应用，它的特点是可以处理大型流数据集。更多信息请查看[Running a Bokeh Server](http://bokeh.pydata.org/en/latest/docs/user_guide/server.html#userguide-server)。

**挂件**

挂件指的是在图形外围的那些元素。如滚动条、下拉式菜单、按钮等都属于挂件。与挂件交互会出发后台的一些函数，从而影响图形中的数据。挂件可以用在独立的Bokeh应用中也可以搭配Bokeh服务器一起使用。更多信息请查看[Adding Interactions](http://bokeh.pydata.org/en/latest/docs/user_guide/interaction.html#userguide-interaction)。

------

### 输出方式-Output Methods

我们可以看到用户指南中遍布的示例中有很多输出文件的方式，最常用的主要是以下几种：

**output_file**

用于生成独立的Bokeh图表HTML文件。

**output_notebook**

用于在Jupyter notebook上嵌入Bokeh图形

**output_server**

用于在一个运行着的Bokeh服务器安装Bokeh应用

这些函数经常回合`show`或者`save`搭配使用。这里是一个例子

```python
from bokeh.plotting import figure, output_file, show

output_file("output.html")

p = figure()
p.line(x=[1, 2, 3], y=[4,6,2])

show(p)
```

Well，假设这个文件叫`foopy`，那么执行`python foo.py`会生成一个包含Bokeh图形的HTML文件。这些函数搭配在交互式设置和从Web应用（如Flask、Django等）中分离出单独的HTML图形文件非常有用。

Bokeh还提供一个强大的命令行工具`bokeh`可以用来生成多种输出。

```
bokeh html
```

根据任何一种Bokeh应用的资源文件（如Python脚本、Bokeh应用目录、JSON文件）生成独立的HTML文件

```
bokeh json
```

根据任何一种Bokeh应用的资源文件生成相当于Bokeh文件的序列化JSON文件。

```
bokeh serve
```

将Bokeh文件作为Web应用发布

用`bokeh`命令的好处是不需要在Python代码中指定输出方式，而通过命令来获得多种格式的输出。也就是一次编写，多次输出。上述的代码也可以简化为

```python
from bokeh.plotting import figure

p = figure()
p.line(x=[1, 2, 3], y=[4,6,2])
```

现在，你就可以用`bokeh html foo.py`来生成独立的HTML文件，或者用`booked serve foo.py`将Bokeh图形以Web应用的形式发布。更多信息请查看[Using bokeh Commands](http://bokeh.pydata.org/en/latest/docs/user_guide/cli.html#userguide-cli)。

### 接口-Interfaces

Bokeh不仅为数据科学家及相关领域的专家提供了快速便捷的接口，还为软件开发者和工程师们提供了更加丰富的接口来配置更多Bokeh成熟的特性。正因为这个特点，Bokeh的方法是分等级的，不同等级的需求、特性对应不同等级的接口方法，而这些方法的使用方法基本都是相同的，这样就可以提高代码的复用率。这一节中主要向用户概述一些用户级的可用接口和一些中心概念。如果你想直接绘制图形，可以跳过这一章，转向[Plotting with Basic Glyphs](http://bokeh.pydata.org/en/latest/docs/user_guide/plotting.html#userguide-plotting)和[Making High-level Charts](http://bokeh.pydata.org/en/latest/docs/user_guide/charts.html#userguide-charts)。

#### bokeh.models

Bokeh实际上是由两个组件库构成的。

第一部分是在浏览器中运行的JavaScript库，BokehJS。这个库负责所有的页面渲染和用户交互。BokehJS的输入是一个用来构成整个网页“轮廓”的JSON对象集。这些对象包括图形、挂件中你能看见的所有东西。这些JSON对象在浏览器中最终会被转换成[Backbone](http://backbonejs.org/)模型，并渲染成对应的[Backbone](http://backbonejs.org/)可视化模型。

第二个部分是Python库（或者其他语言类型的库，这里以Python作为例子），这些库可以生成上述说的JSON对象。这些都是在库的底层完成的，这些Python类可以将代码中设置的内容和属性序列化成JSON对象。所有这些低级模型都可以在**低级**接口[bokeh.models](http://bokeh.pydata.org/en/latest/docs/reference/models.html#bokeh-models)中找到。大多数类都很简单，只有一些属性，设置没有方法。这些属性可以在创建模型的时候传入，或者在之后指定使用该属性的模型。下面以`Rect`标志对象为例给出例子：

```python
# properties can be configured when a model object is initialized
glyph = Rect(x="x", y="y2", w=10, h=20, line_color=None)

# or by assigning values to attributes on the model later
glyph.fill_alpha = 0.5
glyph.fill_color = "navy"
```

类似这样的配置活儿可以普遍的适用于所有Bokeh模型。加上Bokeh接口最终生成的都是模型集，所以所有图形、挂件的风格化和配置都可以通过这一方法来实现，并且不限制于使用的是哪个接口。

使用[bokeh.models](http://bokeh.pydata.org/en/latest/docs/reference/models.html#bokeh-models)接口可以随意搭配图形和挂件，而这样做的坏处就是结果有时候可能并没有意义或者一塌糊涂，但至少，这可以让开发者亲自参与到构建“轮廓”的过程中来。因为这个原因，大多数用户可能更乐意去使用高级接口（下面会介绍到），除非他们有特殊的需求，而高级接口不提供这一需求。关于更多Bokeh模型的知识请移步 [Reference Guide](http://bokeh.pydata.org/en/latest/docs/reference.html#refguide)。

#### bokeh.plotting

plotting接口是Bokeh的**中级**接口，这一接口的使用和[Matplotlib](http://matplotlib.org/)还有[Matlab](http://www.mathworks.com/products/matlab/)中的绘制函数很像。他主要用于让用户选择合适于所用数据的标志，若不指定标志，则图形使用默认的坐标轴、网格线和工具来绘图。所有构建“轮廓”的艰难工序在这一接口中将自动完成。

[bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)接口的中心类是`Figure`类。`Figure`继承自`Plot`，所以也能非常轻松的在图形中添加各类标志。除此之外，`Figure`也能不费吹灰之力就生成默认坐标轴、网格线还有工具。一般来说，用户会通过调用`figure()`函数来创建一个`Figure`对象。

[bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)一个典型的用法如下，在代码的下方附带了对应的图形结果

```python
from bokeh.plotting import figure, output_file, show

# create a Figure object
p = figure(width=300, height=300, tools="pan,reset,save")

# add a Circle renderer to this figure
p.circle([1, 2.5, 3, 2], [2, 3, 1, 1.5], radius=0.3, alpha=0.5)

# specify how to output the plot(s)
output_file("foo.html")

# display the figure
show(p)
```

【图图】

注意观察代码，代码中用了`figure()`创建了图形，之后用`Figure.circle`在图中添加了圆标志。可以看见我们并不需要为配置坐标轴或者网格线而操心（如果需要，也可以自行配置），而且添加工具栏上的工具也只需要传入相应的名字即可。在代码的最后我们用了一些输出函数来将图形展示出来。

> 注意
>
> `output_file()`和`show()`等输出函数可以在[bokeh.io](http://bokeh.pydata.org/en/latest/docs/reference/io.html#bokeh-io)模块中找到，为了方便，这些输出函数也可以从[bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)中导入

除了上面的，其实还有许多用法这里没有展示出来，比如不展示转而保存该图形、风格化或去掉坐标轴和网格线、增加别的曲线并将它们显示在一个图形中等。这些用法的示例你都可以在[User Guide](http://bokeh.pydata.org/en/latest/docs/user_guide.html#userguide)的[Plotting with Basic Glyphs](http://bokeh.pydata.org/en/latest/docs/user_guide/plotting.html#userguide-plotting)这一章中看到。

#### bokeh.charts

[bokeh.charts](http://bokeh.pydata.org/en/latest/docs/reference/charts.html#bokeh-charts)是Bokeh的一个**高级**接口，主要可以快速的绘制一些静态图表。跟[bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)一样，[bokeh.charts](http://bokeh.pydata.org/en/latest/docs/reference/charts.html#bokeh-charts)是通过整合一些较底层的类来简化创建图表的过程。虽然是简化了过程，但是你还是需要提供必要的一些数据，一般情况下，这一接口中的函数是用来创建普通的示意静态图的，[bokeh.charts](http://bokeh.pydata.org/en/latest/docs/reference/charts.html#bokeh-charts)中的函数会自动为不同组的数据标记不同的颜色和其他一些标识。

[bokeh.charts](http://bokeh.pydata.org/en/latest/docs/reference/charts.html#bokeh-charts)中快速绘图的类型包括`Bar()`、`BoxPlot()`、`Histogram()`、`TimeSeries()`（分别对应柱状图、箱图、直方图、时间序列图）等，下面以`Scatter()`作散点图为例给出代码

```python
from bokeh.charts import Scatter, output_file, show

# prepare some data, a Pandas GroupBy object in this case
from bokeh.sampledata.autompg import autompg as df

# create a scatter chart
p = Scatter(df, x='mpg', y='hp', color='cyl',
            title="MPG vs HP (colored by CYL)",
            legend='top_right',
            xlabel="Miles Per Gallon",
            ylabel="Horsepower")

# specify how to output the plot(s)
output_file("chart.html")

# display the figure
show(p)
```

【图图】

需要指出的是输出函数像`output_file()`和`show()`之类的被普遍的用在各个绘图接口中，就像[bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)中也有`output_file()`和`show()`一样。他虽然是定义在[bokeh.io](http://bokeh.pydata.org/en/latest/docs/reference/io.html#bokeh-io)模块中的，但是为了方便也可以从[bokeh.charts](http://bokeh.pydata.org/en/latest/docs/reference/charts.html#bokeh-charts)中导入。

#### 其他接口-Other Interfaces

Bokeh与[Matplotlib](http://matplotlib.org/)具有一定的共存性，你可以用第三方库[mplexporter](https://github.com/mpld3/mplexporter)绘制图形，之后再转化成Bokeh图形，虽然不能100%利用[Matplotlib](http://matplotlib.org/)的特性，但是有时候Bokeh这一特点非常实用。除了刚刚说的[Matplotlib](http://matplotlib.org/)图形，你也可以非常轻易的将用[Seaborn](http://stanford.edu/~mwaskom/software/seaborn/)和[ggplot.py](https://github.com/yhat/ggplot)绘制出来的图形转化成Bokeh图形。下面这个例子只用了一行代码将[Seaborn](http://stanford.edu/~mwaskom/software/seaborn/)图形转化成了Bokeh图形。

```python
import seaborn as sns

from bokeh import mpl
from bokeh.plotting import output_file, show

tips = sns.load_dataset("tips")

sns.set_style("whitegrid")

ax = sns.violinplot(x="day", y="total_bill", hue="sex",
                    data=tips, palette="Set2", split=True,
                    scale="count", inner="stick")

output_file("violin.html")

show(mpl.to_bokeh())
```

【图图】

## <p id="PlottingwithBasicGlyphs">用基础标志绘图-Plotting with Basic Glyphs</p>

### 创建标志-Creating Figures

需要指出的是利用[bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)创建出的图形子带默认的工具和可视化风格。如果要风格化自己的图形请看[Styling Visual Attributes](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling)，若要组合不同工具请看[Configuring Plot Tools](http://bokeh.pydata.org/en/latest/docs/user_guide/tools.html#userguide-tools)。

#### 散点图标atter Markers

要绘制散点图可以用`Figure`中的`circle()`函数：

```python
from bokeh.plotting import figure, output_file, show

# output to static HTML file
output_file("line.html")

p = figure(plot_width=400, plot_height=400)

# add a circle renderer with a size, color, and alpha
p.circle([1, 2, 3, 4, 5], [6, 7, 2, 4, 5], size=20, color="navy", alpha=0.5)

# show the results
show(p)
```

【图图】

照着葫芦画瓢，如果要绘制方形的散点图可以用`Figure`中的`square()`函数：

```python
from bokeh.plotting import figure, output_file, show

# output to static HTML file
output_file("square.html")

p = figure(plot_width=400, plot_height=400)

# add a square renderer with a size, color, and alpha
p.square([1, 2, 3, 4, 5], [6, 7, 2, 4, 5], size=20, color="olive", alpha=0.5)

# show the results
show(p)
```

【图图】

还有许多类型的散点图可供选择，具体见下表（链接中包含例子）

| [`asterisk()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.asterisk) | [`diamond()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.diamond) | [`square_cross()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.square_cross) |
| :--------------------------------------- | :--------------------------------------- | :--------------------------------------- |
| [`circle()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.circle) | [`diamond_cross()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.diamond_cross) | [`square_x()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.square_x) |
| [`circle_cross()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.circle_cross) | [`inverted_triangle()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.inverted_triangle) | [`triangle()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.triangle) |
| [`circle_x()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.circle_x) | [`square()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.square) | [`x()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.x) |
| [`cross()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.cross) |                                          |                                          |

所有类型的图标都有`x`、`y`、`size`（定义在[screen units](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling-units)）和`angle`（默认单位是弧度）。除此之外，[`circle()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.circle)函数具有`radius`参数，用来调节[data-space units](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling-units)。

#### 线形标志-Line Glyphs

##### 单个直线-Single Lines

下面直接给出例子，向`line()`函数传入一系列*x*和*y*值来绘制一根直线：

```python
from bokeh.plotting import figure, output_file, show

output_file("line.html")

p = figure(plot_width=400, plot_height=400)

# add a line renderer
p.line([1, 2, 3, 4, 5], [6, 7, 2, 4, 5], line_width=2)

show(p)
```

【图图】

##### 多条直线-Multiple Lines

有时候需要在同一图形中展示多条曲线，这时可以用`multi_line()`函数：

```python
from bokeh.plotting import figure, output_file, show

output_file("patch.html")

p = figure(plot_width=400, plot_height=400)

p.multi_line([[1, 3, 2], [3, 4, 6, 6]], [[2, 1, 4], [4, 7, 8, 5]],
             color=["firebrick", "navy"], alpha=[0.8, 0.3], line_width=4)

show(p)
```

【图图】

> 注意
>
> 这里绘制函数接收的参数比较特殊，不仅可以接受纯量Python列表，也可以接受元素为列表的列表。

##### 隐藏直线段-Missing Points

`NaN`值可以传入`line()`和`multi_line()`函数。在下面的例子中我们将逻辑上为一条的直线中的一部分隐藏，使其实际上变成两条直线。（实际上我理解的是值为`NaN`的那一段直线就不进行插值了，所以就没有直线）

```python
from bokeh.plotting import figure, output_file, show

output_file("line.html")

p = figure(plot_width=400, plot_height=400)

# add a line renderer with a NaN
nan = float('nan')
p.line([1, 2, 3, nan, 4, 5], [6, 7, 2, 4, 4, 5], line_width=2)

show(p)
```

【图图】

#### 贴图标志-Patch Glyphs

##### 单个贴图-Single Patches

下面的例子示范的是如何向`patch()`函数传入两组一维Python列表来生成单个多边形的贴图。其中两个一维Python列表中的值对应位组成一个点的坐标。

```python
from bokeh.plotting import figure, output_file, show

output_file("patch.html")

p = figure(plot_width=400, plot_height=400)

# add a patch renderer with an alpha an line width
p.patch([1, 2, 3, 4, 5], [6, 7, 8, 7, 3], alpha=0.5, line_width=2)

show(p)
```

【图图】

##### 多个贴图-Multiple Patches

如果要在一个图形中绘制多个贴图，可以使用`patches()`方法，方式如下：

```python
from bokeh.plotting import figure, output_file, show

output_file("patch.html")

p = figure(plot_width=400, plot_height=400)

p.patches([[1, 3, 2], [3, 4, 6, 6]], [[2, 1, 4], [4, 7, 8, 5]],
          color=["firebrick", "navy"], alpha=[0.8, 0.3], line_width=2)

show(p)
```

【图图】

> 注意
>
> 这里绘制函数接收的参数比较特殊，不仅可以接受纯量Python列表，也可以接受元素为列表的列表。

##### 隐藏部分贴图-Missing Points

和`line()`、`multi_line()`一样，`NaN`值也可以被传入`patch()`、`patches()`中。在下面的例子中，我们将一个逻辑上为一块的贴图分成两块（实际上相当于将`NaN`两边的数据分开绘制贴图，只不过这两个贴图颜色一样）：

```python
from bokeh.plotting import figure, output_file, show

output_file("patch.html")

p = figure(plot_width=400, plot_height=400)

# add a patch renderer with a NaN value
nan = float('nan')
p.patch([1, 2, 3, nan, 4, 5, 6], [6, 7, 5, nan, 7, 3, 6], alpha=0.5, line_width=2)

show(p)
```

【图图】

> 警告
>
> Hit testing on patch objects with `NaN` values is not currently supported.

#### 长方形与椭圆形-Rectangles, Ovals and Ellipses

要在图形中绘制和*网格对齐*的四边形可以使用[`quad()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.quad)标志函数，[`quad()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.quad)函数接受`left`、`right`、`top`、`bottom`这四个参数，分别表示四边形的四个边对应的坐标。

```python
from bokeh.plotting import figure, show, output_file

output_file('rectangles.html')

p = figure(width=400, height=400)
p.quad(top=[2, 3, 4], bottom=[1, 2, 3], left=[1, 2, 3],
       right=[1.2, 2.5, 3.7], color="#B3DE69")

show(p)
```

【图图】

如果要绘制任意一种四边形，可以用[`rect()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.rect)函数并指定需要的长、宽、角度来画出需要的标志。

```python
from math import pi
from bokeh.plotting import figure, show, output_file

output_file('rectangles_rotated.html')

p = figure(width=400, height=400)
p.rect(x=[1, 2, 3], y=[1, 2, 3], width=0.2, height=40, color="#CAB2D6",
       angle=pi/3, height_units="screen")

show(p)
```

【图图】

 [`oval()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.oval)标志函数可接受的参数与[`rect()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.rect)一样。

```python
from math import pi
from bokeh.plotting import figure, show, output_file

output_file('ovals.html')

p = figure(width=400, height=400)
p.oval(x=[1, 2, 3], y=[1, 2, 3], width=0.2, height=40, color="#CAB2D6",
       angle=pi/3, height_units="screen")

show(p)
```

【图图】

 [`ellipse()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.ellipse)标志函数接受的参数和 [`oval()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.oval)、[`rect()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.rect)并无二样，个人感觉 [`ellipse()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.ellipse)和 [`oval()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.oval)函数绘制的都是椭圆形，只是[`ellipse()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.ellipse)绘制的椭圆形更胖一点。

```python
from math import pi
from bokeh.plotting import figure, show, output_file

output_file('ellipses.html')

p = figure(width=400, height=400)
p.ellipse(x=[1, 2, 3], y=[1, 2, 3], width=[0.2, 0.3, 0.1], height=0.3,
          angle=pi/3, color="#CAB2D6")

show(p)
```

【图图】

#### 图片-Images

要在图形中显示自己的图片，可以用[`image()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.image)、 [`image_rgba()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.image_rgba)和[`image_url()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.image_url) 标志函数。

下面这个例子演示如何用[`image_rgba()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.image_rgba)在图形中嵌入raw RGBA数据图。

> 注意
>
> 这个例子中使用Numpy库来简化数据的生成

```python
from __future__ import division

import numpy as np

from bokeh.plotting import figure, output_file, show

# create an array of RGBA data
N = 20
img = np.empty((N, N), dtype=np.uint32)
view = img.view(dtype=np.uint8).reshape((N, N, 4))
for i in range(N):
    for j in range(N):
        view[i, j, 0] = int(255 * i / N)
        view[i, j, 1] = 158
        view[i, j, 2] = int(255 * j / N)
        view[i, j, 3] = 255

output_file("image_rgba.html")

p = figure(plot_width=400, plot_height=400, x_range=(0, 10), y_range=(0, 10))

p.image_rgba(image=[img], x=[0], y=[0], dw=[10], dh=[10])

show(p)
```

【图图】

#### 线段与射线-Segments and Rays

有时候在一个图形中绘制多个线段或者射线会非常有用，Bokeh提供了 [`segment()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.segment)和[`ray()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.ray)标志函数来完成这一需求。

 [`segment()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.segment)函数接受`x0`、`y0`、`x1`、`y1`（分别对应起始x，y坐标和终点x，y坐标）

```python
from bokeh.plotting import figure, show

p = figure(width=400, height=400)
p.segment(x0=[1, 2, 3], y0=[1, 2, 3], x1=[1.2, 2.4, 3.1],
          y1=[1.2, 2.5, 3.7], color="#F4A582", line_width=3)

show(p)
```

【图图】

 [`ray()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.ray)函数接受`x`、`y`、`length`、`angle`（分别表示起始x，y坐标、长度、角度）这几个参数。其中角度的默认单位为“弧度”（但也可以用角度），长度单位为[屏幕像素](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling-units)，如果要绘制无限长的射线，将`0`传给`length`参数。

```python
from bokeh.plotting import figure, show

p = figure(width=400, height=400)
p.ray(x=[1, 2, 3], y=[1, 2, 3], length=45, angle=[30, 45, 60],
      angle_units="deg", color="#FB8072", line_width=2)

show(p)
```

#### 楔形与弧形-Wedges and Arcs

[`arc()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.arc)标志函数能够绘制简单的弧形，他接受`radius`、`start_angle`和`end_angle`（分别表示半径、起始角度、终点角度，上面例子中的角度的单位是弧度），该函数还有个可选参数`direction`，可以传入`"clock"`（顺时针绘制）或者`"anticlock"`（逆时针绘制）参数。

```python
from bokeh.plotting import figure, show

p = figure(width=400, height=400)
p.arc(x=[1, 2, 3], y=[1, 2, 3], radius=0.1, start_angle=0.4, end_angle=4.8, color="navy")

show(p)
```

【图图】

 [`wedge()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.wedge)函数接受的参数和[`arc()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.arc)一样，但是其绘制的是扇形。

```python
from bokeh.plotting import figure, show

p = figure(width=400, height=400)
p.wedge(x=[1, 2, 3], y=[1, 2, 3], radius=0.2, start_angle=0.4, end_angle=4.8,
        color="firebrick", alpha=0.6, direction="clock")

show(p)
```

【图图】

 [`annular_wedge()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.annular_wedge)函数和[`arc()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.arc)函数很像，但绘制的图形是环形， [`annular_wedge()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.annular_wedge) 接受`inner_radius`和`outer_radius`参数（分别对应内半径和外半径），而非`radius`。

```python
from bokeh.plotting import figure, show

p = figure(width=400, height=400)
p.annular_wedge(x=[1, 2, 3], y=[1, 2, 3], inner_radius=0.1, outer_radius=0.25,
                start_angle=0.4, end_angle=4.8, color="green", alpha=0.6)

show(p)
```

【图图】

最后是[`annulus()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.annulus)标志函数，该函数只能绘制整个环形，用法如下。

```python
from bokeh.plotting import figure, show

p = figure(width=400, height=400)
p.annulus(x=[1, 2, 3], y=[1, 2, 3], inner_radius=0.1, outer_radius=0.25,
          color="orange", alpha=0.6)

show(p)
```

【图图】

#### 特殊曲线-Specialized Curves

Bokeh还提供了[`quadratic()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.quadratic)和[`bezier()`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh.plotting.figure.Figure.bezier)标志函数来绘制二次和三次曲线。有时候还有一些特例情况，详情请看[reference documentation](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)。

### 组合标志-Combining Multiple Glyphs

要在同一图形中绘制多种标志可以直接在图形对象（`Figure`)中添加。

```python
rom bokeh.plotting import figure, output_file, show

x = [1, 2, 3, 4, 5]
y = [6, 7, 8, 7, 3]

output_file("multiple.html")

p = figure(plot_width=400, plot_height=400)

# add both a line and circles on the same plot
p.line(x, y, line_width=2)
p.circle(x, y, fill_color="white", size=8)

show(p)
```

【图图】

所有在[bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)中的标志函数都遵循这一原则，同一个图形中可以添加任意多个标志。

### 设置坐标范围-Setting Ranges

一般情况下，Bokeh

### 配置坐标轴-Specifying Axis Types

#### 分组坐标轴-Categorical Axes

#### 时序坐标轴-Datetime Axes

#### 对数坐标轴-Log Scale Axes

#### 双轴-Twin Axes

### 添加注释

## <p id="EmbeddingPlotsandApps">嵌入图表和Apps-Embedding Plots and Apps</p>

原文 [Embedding Plots and Apps](http://bokeh.pydata.org/en/latest/docs/user_guide/embed.html)

Bokeh提供了多种方式来为HMTL插入图表

### 生成单独的HTML文件

Bokeh的`file_html()`函数能生成包含图表的独立HTML文件，该文件的模板能用Bokeh自带的，也可以用自己的（具体自己查阅`file_html()`函数的文档，例子 [gapminder example plot](https://github.com/bokeh/bokeh/blob/master/examples/howto/interactive_bubble/gapminder.py)）。HTML文件包含了图表的所有信息并且是可移植的，同时每张图表旁边的交互工具不会消失。

例子：

```python
from bokeh.plotting import figure
from bokeh.resources import CDN
from bokeh.embed import file_html

plot = figure()
plot.circle([1,2], [3,4])

html = file_html(plot, CDN, "my plot")
```

其中，`html`中的文本可以用Python自带函数保存到一个文件中

> 注意
>
> 这个方法相对比较低级、直接，在后面的内容中会教大家用`bokeh.plotting`和`bokeh.charts`中的接口配合[`output_file()`](http://bokeh.pydata.org/en/latest/docs/reference/io.html#bokeh.io.output_file)、[`show()`](http://bokeh.pydata.org/en/latest/docs/reference/io.html#bokeh.io.show)、[`save()`](http://bokeh.pydata.org/en/latest/docs/reference/io.html#bokeh.io.save)函数来达到相同的效果

### 作为组件嵌入到HTML中

Bokeh提供`components()`函数来生成组件形式的图标代码。`components()`返回

- 一个`<script>`标签代码段（包含所有图表数据）
- 一个`<div>`标签代码段（包含引用`<script>`的代码）

例子：

```python
from bokeh.plotting import figure
from bokeh.embed import components

plot = figure()
plot.circle([1,2], [3,4])

script, div = components(plot)
```

其中`script`长这样

```html
<script type="text/javascript">
    $(function() {
        var modelid = "fba97329-a355-499e-9252-0adc64b19d2e";
        var modeltype = "Plot";
        var elementid = "8ed68feb-d258-4953-9dfb-fb1c13326509";
        Bokeh.logger.info("Realizing plot:")
        Bokeh.logger.info(" - modeltype: Plot");
        Bokeh.logger.info(" - modelid: fba97329-a355-499e-9252-0adc64b19d2e");
        Bokeh.logger.info(" - elementid: 8ed68feb-d258-4953-9dfb-fb1c13326509");

        var all_models = [ JSON PLOT MODELS AND DATA ARE HERE ];

        Bokeh.load_models(all_models);
        var model = Bokeh.Collections(modeltype).get(modelid);
        var view = new model.default_view({
            model: model, el: '#8ed68feb-d258-4953-9dfb-fb1c13326509'
        });
        Bokeh.index[modelid] = view
    });
</script>
```

`div`长这样

```html
<div class="plotdiv" id="8ed68feb-d258-4953-9dfb-fb1c13326509"></div>
```

得到了`script`和`div`之后还不能够显示图表，还需将Bokeh官方的`.css`和`.js`文件引用过来才行，也可以将官方的文件下载到本地来加载。引用只需要在`<head>`标签中加入如下代码

```html
<link
    href="http://cdn.pydata.org/bokeh/release/bokeh-x.y.z.min.css"
    rel="stylesheet" type="text/css">
<link
    href="http://cdn.pydata.org/bokeh/release/bokeh-widgets-x.y.z.min.css"
    rel="stylesheet" type="text/css">

<script src="http://cdn.pydata.org/bokeh/release/bokeh-x.y.z.min.js"></script>
<script src="http://cdn.pydata.org/bokeh/release/bokeh-widgets-x.y.z.min.js"></script>
```

其中文件名中有"-widget"的引用文件只有在你需要用到**Bokeh widgets**时才会用到，平时可以不引用来节省页面加载的时间。的`x.y.z`指的是版本号，比如现在要引用**0.12.0**版本的Bokeh，则代码应该长这样

```html
<link
    href="http://cdn.pydata.org/bokeh/release/bokeh-0.12.0.min.css"
    rel="stylesheet" type="text/css">
<link
    href="http://cdn.pydata.org/bokeh/release/bokeh-widgets-0.12.0.min.css"
    rel="stylesheet" type="text/css">

<script src="http://cdn.pydata.org/bokeh/release/bokeh-0.12.0.min.js"></script>
<script src="http://cdn.pydata.org/bokeh/release/bokeh-widgets-0.12.0.min.js"></script>
```

> 注意
>
> <script>标签不能省略结束标签</script>不然可能会加载失败

例子：

一个完整的HTML文件长这样

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title>Bokeh Scatter Plots</title>

        <link rel="stylesheet" href="http://cdn.pydata.org/bokeh/release/bokeh-0.12.0.min.css" type="text/css" />
        <script type="text/javascript" src="http://cdn.pydata.org/bokeh/release/bokeh-0.12.0.min.js"></script>

        <!-- SCRIPT文本放这COPY -->

    </head>
    <body>
        <!-- DIV文本放这 -->
    </body>
</html>
```

`component()`函数能接受单个Bokeh图表模型作为参数，也能接受包含Bokeh图表模型的列表（List）、元组（tuple）、字典（dictionary）作为参数，其返回值是包含`script`和`div`文本的对应数据结构。

### 在IPython Notebook中嵌入图表

`notebook_div()`函数能够生成适用于IPython Notebook嵌入的文本包，即只有一个输出。文本包中包含`script`和`div`文本。

```python
from bokeh.plotting import figure
from bokeh.embed import notebook_div

plot = figure()
plot.circle([1,2], [3,4])

div = notebook_div(plot)
```

返回的内容和`components()`大体相同，这里不再显示出来

> 注意
>
> 这个方法相对比较低级、直接，在后面的内容中会教大家用`bokeh.plotting`和`bokeh.charts`中的接口配合 [`output_notebook()`](http://bokeh.pydata.org/en/latest/docs/reference/io.html#bokeh.io.output_notebook)、[`save()`](http://bokeh.pydata.org/en/latest/docs/reference/io.html#bokeh.io.save)函数来达到相同的效果

### 自动加载的嵌入方式

Bokeh提供了一种自动加载的方式来嵌入图表，自动加载的形式是将一段`<script>`标签文本插入到`<body>`标签中，运行时`<script>`文本会自动替换成`<div>`文本。（这种方式需要引用官方的`.css`和`.js`文件，引用方式上面提到过了）

下面有两个不同的例子

#### 从服务器获取数据

这种方法是将数据用`autoload_server()`函数存进Bokeh服务器（Bokeh server）中

例子

```python
from bokeh.client import push_session
from bokeh.embed import autoload_server
from bokeh.plotting import figure, curdoc

# figure() function auto-adds the figure to curdoc()
plot = figure()
plot.circle([1,2], [3,4])

session = push_session(curdoc())
script = autoload_server(plot, session_id=session.id)
```

`script`文本长这样

```html
<script
src="http://localhost:5006/autoload.js?bokeh-autoload-element=82ae93bf-79c2-4028-af7e-1cf6b1a0ea1a&bokeh-session-id=qjPGXLj7UWx7G9LDkwEq48fMOcxQfepxW7HUYPCQNrmN"
id="82ae93bf-79c2-4028-af7e-1cf6b1a0ea1a"
data-bokeh-model-id="b08c02c4-f93c-461c-bb23-514b54dfec83"
data-bokeh-doc-id=""
></script>
```

> 注意
>
> 要让script文本执行得要Bokeh server处于运行状态

如果你已经有app在Bokeh服务器上并且还有app的url，那么替换代码如下

```python
script = autoload_server(model=None, app_path="/apps/slider", url="https://demo.bokehplots.com")
```

更多细节参见 [autoload_server()](http://bokeh.pydata.org/en/latest/docs/reference/embed.html#bokeh.embed.autoload_server)

#### 从静态文件中获取数据

如果不想使用Bokeh服务器的话，也可以用`autoload_static()`函数生成引用静态数据的`<script>`代码段。

例子

```python
from bokeh.resources import CDN
from bokeh.plotting import figure
from bokeh.embed import autoload_static

plot = figure()
plot.circle([1,2], [3,4])

js, tag = autoload_static(plot, CDN, "some/path")
```

这里的`script`文本长这样

```html
<script
    src="some/path"
    id="c5339dfd-a354-4e09-bba4-466f58a574f1"
    async="true"
    data-bokeh-data="static"
    data-bokeh-modelid="7b226555-8e16-4c29-ba2a-df2d308588dc"
    data-bokeh-modeltype="Plot"
    data-bokeh-loglevel="info"
></script>
```

`script`文本要保存在能够索引到“`some/path`"的路径上的HTML中

> 注意
>
> 由于<script>会被替换成<div>所以不能把<script>代码段放在<head>标签中

