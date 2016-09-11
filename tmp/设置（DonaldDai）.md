## 设置（Getting Set Up）

这一章的第一部分会指引你快速安装一下Bokeh并做一些小测试来检测一下是否安装正常。

### 安装Bokeh库

安装Bokeh最简单的方法就是用诸如`pip`、`conda`等包管理工具来安装。如果你用过 [Anaconda](http://continuum.io/anaconda)那么你可以用`conda`来安装

```
conda install bokeh
```

否则，就用`pip`工具来安装

```
pip install bokeh
```

如果要查看更多安装方面的细节可以参考Bokeh文档的[安装](http://bokeh.pydata.org/en/latest/docs/installation.html#installation)部分。

### 验证安装

第一步你可以在Python的交互式命令行中`import bokeh`，用`bokeh.__version__`来查看当前安装的版本。如果你能成功执行命令，结果应该长这样：

【图图】

第二步，你可以用Bokeh绘制一个简单的图形来检测是否安装正常。将下面的代码保存到文件中并执行或者直接在Python交互式命令行中键入下面的代码来绘制一副简单的图形。

```python
from bokeh.plotting import figure, output_file, show
output_file("test.html")
p = figure()
p.line([1, 2, 3, 4, 5], [6, 7, 2, 4, 5], line_width=2)
show(p)
```

这段代码会生成一个名为`test.html`的本地文件，并且会自动打开默认浏览器来显示图形。正常运行的图形应该是这样的

【图图】

你也可以在IPython/Jupyter notebook中执行上述的代码来绘制图形，但是需要把上面代码中的`output_file`替换成`output_notebook`。结果如下

【图图】

### 寻求帮助？

如果在你安装或者运行示例的时候出现问题了，可以发Email到[Bokeh mailing list](https://groups.google.com/a/continuum.io/forum/#!forum/bokeh)寻求帮助，也可以在[Bokeh GitHub issue tracker](https://github.com/bokeh/bokeh/issues)中提交Issue。