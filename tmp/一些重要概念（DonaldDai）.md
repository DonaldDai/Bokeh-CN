## 一些重要概念

### 术语表

为了更好的使用用户指南，了解相关高级概念很重要。下面是一份小术语表，上面介绍了一些Bokeh的重要概念

------

**应用**

Bokeh应用指的是一个已经渲染过的文件，结果一般运行在浏览器中。

**Bokeh JS文件**

Bokeh的Javascript文件主要用于渲染图形和UI中的交互工具。一般用户不需要考虑JS文件中的内容，但如果你有一些JS的知识，那最好不过啦。更多细节可以查看[开发者指南](http://bokeh.pydata.org/en/latest/docs/dev_guide.html#devguide)中的[BokehJS](http://bokeh.pydata.org/en/latest/docs/dev_guide/bokehjs.html#devguide-bokehjs)。

**图表**

示例中的静态图如柱状图，水平延伸的图和时间序列图等都可以由Bokeh提供的`bokeh.charts`高级接口来快速构建。更多示例及用法请查看 [构建高级图表](http://bokeh.pydata.org/en/latest/docs/user_guide/charts.html#userguide-charts)。

**文件**

文件指的是Bokeh应用所使用的数据集。文件中包含Bokeh应用渲染图表和交互工具所要用到的所有模型和数据。

**嵌入**

嵌入指的是在Web应用、网页或者Jupyter（Ipython） Notebook中插入Bokeh的图标。更多细节请查看 [插入图表或Apps](http://bokeh.pydata.org/en/latest/docs/user_guide/embed.html#userguide-embed)。

**标志**

标志是构建Bokeh图形的基础元素，如曲线、三角形、方形、楔形、图示等都属于标志。`bokeh.plotting`接口提供了便捷的方法创建自定义标志。更多细节请查看 [Plotting with Basic Glyphs](http://bokeh.pydata.org/en/latest/docs/user_guide/plotting.html#userguide-plotting)。

**模型**

模型是Bokeh中最底层的对象，模型的作用就是组成Bokeh应用的整个“轮廓（scenegraphs）”。这些对象在`bokeh.models`接口里。大多数的用户不会直接接触到这些底层的对象。然而最终的Bokeh应用是由这些对象的集合组成的，所以理解它也是非常重要的，这样你可以更随心所欲的绘制Bokeh图形。更多信息请查看[Styling Visual Attributes](http://bokeh.pydata.org/en/latest/docs/user_guide/styling.html#userguide-styling)。

**Bokeh服务器**

Bokeh服务器是一个可选项，即使不使用Bokeh可以在浏览器中渲染交互图形。Bokeh服务器主要用于发布或分享交流Bokeh图形或者应用，它的特点是可以处理大型流数据集。更多信息请查看[Running a Bokeh Server](http://bokeh.pydata.org/en/latest/docs/user_guide/server.html#userguide-server)。

**挂件**

挂件指的是在图形外围的那些元素。如滚动条、下拉式菜单、按钮等都属于挂件。与挂件交互会出发后台的一些函数，从而影响图形中的数据。挂件可以用在独立的Bokeh应用中也可以搭配Bokeh服务器一起使用。更多信息请查看[Adding Interactions](http://bokeh.pydata.org/en/latest/docs/user_guide/interaction.html#userguide-interaction)。

-----

### 输出方式-Output Methods

我们可以看到用户指南中遍布的示例中有很多输出文件的方式，最常用的主要是以下几种：

`**output_file**`

用于生成独立的Bokeh图表HTML文件。

### 接口-Interfaces

#### bokeh.models

#### bokeh.plotting

#### bokeh.charts

#### 其他接口-Other Interfaces



