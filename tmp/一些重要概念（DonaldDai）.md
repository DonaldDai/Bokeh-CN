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

-----

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

