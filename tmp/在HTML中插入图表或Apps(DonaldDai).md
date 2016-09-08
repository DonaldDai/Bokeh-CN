## 在HTML中嵌入图表和Apps

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
> 由于<script>会替换成<div>所以不能把<script>代码段放在<head>标签中