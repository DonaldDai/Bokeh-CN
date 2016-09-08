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
- Quickstart
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