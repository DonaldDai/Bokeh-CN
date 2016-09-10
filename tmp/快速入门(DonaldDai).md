## 快速入门(Quickstart)

原文 [Quickstart](http://bokeh.pydata.org/en/latest/docs/user_guide/quickstart.html)

### 介绍

Bokeh是致力于网页浏览器展示的Python交互式图表库。Bokeh能读取巨大的数据集或者流数据以简单快捷的方式为网页提供优美、简洁、高交互性能的图形。

为了能让用户高度自定义简单、高性能、灵活的图表，Bokeh开放三个层次的接口给用户：

-  [`bokeh.models`](http://bokeh.pydata.org/en/latest/docs/reference/models.html#bokeh-models)   低级接口，能为app开发者提供高度灵活的图形表示（可以自定义一些顶层的组件）
-  [`bokeh.plotting`](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)  中级接口，该接口主要用于绘制曲线（默认加载一些低级的组件）
-  [`bokeh.charts`](http://bokeh.pydata.org/en/latest/docs/reference/charts.html#bokeh-charts) 高级接口，能快速简单地构建复杂的图形

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

>注意
>
>pip安装方式不安装示例。若要查看示例可以`Clone`下Git仓库中的`examples/`到本地。[HELP此处应有超链接]

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

【图图】

#### 数据联动的两种方式

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

【图图】

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

选择方形选择工具（box select）或者套索选择工具（lasso select）在其中一个图形中进行操作，这个操作会联动另一个图形。

#### 时间序列图形

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

【图图】

### Bokeh图形服务器

Bokeh服务器是一个可选的组件项。尽管没有Bokeh图形服务器，我们一样可以创建出有趣、可交互的可视化数据。但是Bokeh还有一些新颖、强大的能力或许你会想用到

- 用UI和选项来驱动图形的计算和更新
- 能够降低大型数据集采样率的智能服务端
- 通过流数据自动更新图形
- 适用于大数据的成熟图形重绘系统
- 发布更易于普通用户操作的可视化图形

由于空间有限，不能在快速入门中讲解所有的用法，读者可以现在下面这个例子中感受一些Bokeh图形服务器的强大。

【交互图图】

你可以在 [Gallery](http://bokeh.pydata.org/en/latest/docs/gallery.html#gallery)的 [Server App Examples](http://bokeh.pydata.org/en/latest/docs/gallery.html#gallery-server-examples)部分中找到更多有关图形服务器绘图的例子。想要知道更多图形服务器的细节请移步 [User Guide](http://bokeh.pydata.org/en/latest/docs/user_guide.html#userguide)的[Running a Bokeh Server](http://bokeh.pydata.org/en/latest/docs/user_guide/server.html#userguide-server)部分

### 下一步干啥？

【困了。睡觉。。。】

