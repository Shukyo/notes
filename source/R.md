## R相关笔记


### ggplot相关知识点


#### ggplot2常用包

| 使用            | 介绍                                |
| --------------- | ----------------------------------- |
| library(ggsci)  | 使用杂志惯用颜色进行配色            |
| library(ggmisc) | 可在绘制趋势图时候直接添加R^2或公式 |
| library(gg.gap) | 可对坐标轴进行截断                  |

#### 坐标系统
1. 需要添加第二坐标轴
  ```R
  scale_y_continuous(...,sec.axis=dup_axis(~.)

  # 需要在离散变量的第二坐标轴上添加label(scale_y_discrete不支持sec.axis)
  # 将离散变量强制转化成连续变量
  scale_y_continuous(breaks = 1:length(levels(dat$col1)),labels= levels(levels(dat$col1)),
                      sec.axis = dup_axis(labels=dat[match(levels(dat$col1),dat$col1),]$col2))
  ```

#### 颜色系统
1. 使用默认颜色，但需要定制其中某个颜色
  ```R
  gg_color_hue <- function(n) {
    hues = seq(15, 375, length = n + 1)
    hcl(h = hues, l = 65, c = 100)[1:n]
  }
  pal<-gg_color_hue(10)
  pal[3]<-"white"
  scale_color_manual(values=pal)
  ```

#### 散点图
1. 绘制散点图时，需要添加趋势线和R2值
  ```R
  library(ggpmisc)
  ggplot(...)+geom_point() +
  geom_smooth(method = "lm") +
  stat_poly_eq(aes(label= ..rr.label..),formula =y~x ,parse=T,size=4,na.rm=T)
  ```

#### 累积曲线图
1. 绘制累积曲线图
  ```R
  ggplot(...) + geom_step(aes(y=..y..),stat="ecdf") 
  ```

#### 柱状图
1. 绘制柱状图时，使用比例而非count数绘图
  ```R
  ggplot() + geom_bar(aes(y,..prop..,group=1,fill=factor(..prop..)),stat="count",show.legend=F)
  #OR
  ggplot() + geom_bar(aes(x,fill=group),position = "fill")
  ```

2. 使用geom_bar时设置ylim
  ```R
  #使用ylim直接设置时，柱状图不显示
  p+geom_bar(stat="identity")+coord_cartesian(ylim=c(1,2))
  ```

#### ggplot中使用变量
```R
 x="variable"
 ggplot(aes(.data[[x]]))
```
