---
title: "办公自动化之，用ggplot发图表给你"
output: html_document
---

```
library(ggplot2)
library(reshape2)
```

有没曾遇到过这样的情况，想要看些统计图表，公司的报表系统操作却很繁琐。Excel倒是很自主，久而久之发现每天重复工作量太大。用ggplot吧，你将有更多自主权，而它上手其实很容易。

作为R的第三方包，ggplot一直名列前茅。在Hadley的ggplot2官方文档中, Hadely这样对Wilkinson的图形语法进行了描述：“一张统计图形就是从数据到几何对象(geometric object, 缩写为geom, 包括点、线、条形等)的图形属性(aesthetic attributes, 缩写为aes, 包括颜色、形状、大小等)的一个映射。此外, 图形中还可能包含数据的统计变换(statistical transformation, 缩写为stats), 最后绘制在某个特定的坐标系(coordinate system,  缩写为coord)中, 而分面(facet, 指将绘图窗口划分为若干个子窗口)则可以用来生成数据中不同子集的图形。”因此在ggplot2中, 图形语法中至少包括了如下几个图形部件：

数据(data)
映射(mapping)
几何对象(geom)
统计变换(stats)
标度(scale)
坐标系(coord)
分面(facet)
    这些组件之间是通过“+”, 以图层(layer)的方式来粘合构图的, 所以图层是ggplot2中一个重要的概念。当然, 在掌握基本的图形部件基础上, 要完成一幅高质量的统计绘图, 仍然需要其他图形部件来进一步扩展, 这包括了：

主题(theme)
存储和输出
    接下来将对这些在ggplot2包中出现的概念逐一展开 
    
## 数据(data)

1. 在ggplot2中, 所接受的数据集必须为数据框(data.frame)格式, 如内置的mtcars数据集：  
```
head(cars)
```
2. 这种格式带来的好处是数据易于存储,也能在保留原有的绘图参数下,用%+%方便地变更已有数据集。通过”+”以图层的方式加入点的几何对象   
```p <- ggplot(mtcars, aes(mpg, wt, colour = cyl)) +
  geom_point() #geom_point()为通过”+”以图层的方式加入点的几何对象
p
mtcars.c <- transform(mtcars, mpg = mpg^2)
p %+% mtcars.c #用mtcars.c替换mtcars
```  

3. 而ggplot2进行数据分组时必须根据行, 而不能根据列, 例如在mtcars的数据集中, 可以把汽车按汽缸数进行分组,但不能按汽车的档位数和汽缸数这两个变量分为两组。这要求把“宽”数据转化为“长”数据。所谓的长数据是变量不在是放在各个列上, 而是拍成一列, 每一个变量都分别占其中的几行,这样就能方便的对每个变量进行分组。reshape2中melt()和cast()能够灵活的融合(melt)和重铸(cast)在数据框中的数据。  
```#融合档位数和汽缸数这两个变量
mtcars.m <- melt(mtcars, id = c("mpg", "disp", "hp", "drat", "wt", "qsec", "vs", "carb")) 
head(mtcars)
head(mtcars.m)
```
更多请参考：http://www.cellyse.com/how_to_use_gggplot2_part1/  
既然要发出邮件，那么图片导出功能就是很重要的了   

## 输出(ggsave)

ggsave()是ggplot2种特有的输出函数,是一种极为方便的出图方式，把图片插入相应的html页面文档里，设置好crontab定时任务，你就可以定时收到邮件了，被动的接受几次数据，相信你对数据的理解也自然的增强了。

```p <- ggplot(mtcars, aes(x = mpg, y = disp)) + geom_point()
ggsave(file = "mtcars_plot.png", width = 5, height = 6, type = "cairo", dpi = 600) 
#cairo为抗锯齿包, ggplot默认输出即为cairo处理
```

