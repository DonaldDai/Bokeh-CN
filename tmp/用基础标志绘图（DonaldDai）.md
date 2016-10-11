## 用基础标志绘图-Plotting with Basic Glyphs

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

一般情况下，Bokeh会根据曲线标志自适应的设置坐标范围，但你也可以用`Rangeld`方法来改变`x_range`和`y_range`来设置坐标范围，`Rangeld`方法接受两个参数，分别为坐标的起始点和终点。

```python
p.x_range = Rangeld(0, 100)
```

为方便起见，`figure()`方法也能接受形式为（起始点，终点）的元组作为属性`x_range`或`y_range`的值，而这两个属性能改变图形的坐标轴范围，下面的例子演示了两种修改坐标轴范围的方法

```python
from bokeh.plotting import figure, output_file, show
from bokeh.models import Range1d

output_file("title.html")

# create a new plot with a range set with a tuple
p = figure(plot_width=400, plot_height=400, x_range=(0, 20))

# set a range using a Range1d
p.y_range = Range1d(0, 15)

p.circle([1, 2, 3, 4, 5], [2, 5, 8, 2, 7], size=10)

show(p)
```

【图图】

你也可以设置一个范围，限制用户使用pan或zoom工具的范围

### 配置坐标轴-Specifying Axis Types

上面所有的例子所使用的坐标轴都是线性的。线性坐标轴适用于大多数图形，但有时候时间轴和对数轴更有用，这一节中将讲述如何配置[bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)图形的坐标轴类型。

#### 类轴-Categorical Axes

```python
from bokeh.plotting import figure, output_file, show

factors = ["a", "b", "c", "d", "e", "f", "g", "h"]
x = [50, 40, 65, 10, 25, 37, 80, 60]

output_file("categorical.html")

p = figure(y_range=factors)

p.circle(x, factors, size=15, fill_color="orange", line_color="green", line_width=3)

show(p)
```

【图图】

#### 时间坐标轴-Datetime Axes

当处理的数据与时间有关时，使用时间坐标轴是个很好的选择。

> 注意
>
> 下面的例子需要联网才能正常运行，并且，为了更方便的展示数据，会用到第三方Pandas库。

之前我们已经学习过了如何使用[bokeh.plotting](http://bokeh.pydata.org/en/latest/docs/reference/plotting.html#bokeh-plotting)的`figure()`函数来绘制图形，其实`figure()`函数还接受`x_axis_type`和`y_axis_type`参数，分别表示x和y轴的类型。要配置成时间坐标轴，传入`"datetime"`参数即可。

```python
import pandas as pd
from bokeh.plotting import figure, output_file, show

AAPL = pd.read_csv(
        "http://ichart.yahoo.com/table.csv?s=AAPL&a=0&b=1&c=2000&d=0&e=1&f=2010",
        parse_dates=['Date']
    )

output_file("datetime.html")

# create a new plot with a datetime axis type
p = figure(width=800, height=250, x_axis_type="datetime")

p.line(AAPL['Date'], AAPL['Close'], color='navy', alpha=0.5)

show(p)
```

【图图】

> 注意 
>
> 未来版本的Bokeh将会自动识别时间序列数据，并配置时间坐标轴

#### 对数坐标轴-Log Scale Axes

当处理指数级增长等快速增长的数据时，用指数坐标轴能更准确方便的表示图形，有的情况数据增长的很快，以致于两个轴都要用指数坐标轴来表示。

和上面的方法类似，要配置指数坐标轴，向`figure()`函数的`x_axis_type`和`y_axis_type`属性传入`"log"`值即可。

```python
from bokeh.plotting import figure, output_file, show

x = [0.1, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0]
y = [10**xx for xx in x]

output_file("log.html")

# create a new plot with a log axis type
p = figure(plot_width=400, plot_height=400,
           y_axis_type="log", y_range=(10**-1, 10**4))

p.line(x, y, line_width=2)
p.circle(x, y, fill_color="white", size=8)

show(p)
```

【图图】

#### 双轴-Twin Axes

有的情况下要将两个范围不同的曲线表示在同一图形中，这时就需要两个坐标轴，也就是双轴。可以通过图形对象的`extra_x_range`和`extra_y_range`属性来创建额外的坐标轴，再通过`add_layout`函数布置到图形中，例子如下

```python
from numpy import pi, arange, sin, linspace

from bokeh.plotting import output_file, figure, show
from bokeh.models import LinearAxis, Range1d

x = arange(-2*pi, 2*pi, 0.1)
y = sin(x)
y2 = linspace(0, 100, len(y))

output_file("twin_axis.html")

p = figure(x_range=(-6.5, 6.5), y_range=(-1.1, 1.1))

p.circle(x, y, color="red")

p.extra_y_ranges = {"foo": Range1d(start=0, end=100)}
p.circle(x, y2, color="blue", y_range_name="foo")
p.add_layout(LinearAxis(y_range_name="foo"), 'left')

show(p)
```

【图图】

### 添加注释

这一部分已被移除，具体详见[Adding Annotations](http://bokeh.pydata.org/en/latest/docs/user_guide/annotations.html#userguide-annotations)。