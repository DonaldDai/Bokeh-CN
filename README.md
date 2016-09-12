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

例子结果能不显示在Makedown中，是否要链接到外网上？

# Bokeh中文用户指南

目录

- <a href="#UserGuide">用户指南-User Guide</a>
- <a href="#Quickstart">快速入门-Quickstart</a>
- <a href="#GettingSetUp">设置-Getting Set Up</a>
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
- <a href="#EmbeddingPlotsandApps">在HTML中嵌入图表和Apps-Embedding Plots and Apps</a>
- Speeding up with WebGL
- Mapping Geo Data
- Developing with JavaScript
- Extending Bokeh
- Learning More
- Tutorials

## <p id="UserGuide">用户指南（User Guide）</p>

这一章内容主要是了解一下整片用户指南的大体结构，根据你可能用到的情况，你可以挑选不同的章节去了解。章节根据内容分为：

### 快速入门（Quickstart）

主要是走马观花的带你过一遍基本的功能和用法。

### 设置（Getting Set Up）

验证你的Bokeh是否安装成功

### 在HTML中插入图表或Apps（Embedding Plots and Apps)

以多种方式在HTML文档中嵌入静态或基于Bokeh服务器的交互图表

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

## <p id="EmbeddingPlotsandApps">在HTML中嵌入图表和Apps-Embedding Plots and Apps</p>

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

