# Flex布局

传统布局基于盒模型，对特殊布局不方便实现比如垂直居中布局。而flex布局可以简便，完整，响应式地实现各种页面布局。

* 任何一个容器都可以使用flex布局，包括行内元素(Webkit内核的浏览器需要加上-Webkit前缀)

```css
.box{
    display:flex
}
.box{
    display:inline-flex
}
.box{
  display: -webkit-flex; /* Safari */
  display: flex;
}
```

### 基本概念

采用flec布局的元素称为flex容器，他的子元素称为flex项目。容器默认存在两根轴，水平的主轴和垂直的交叉轴。单个项目占据主轴的空间叫main size，占据交叉轴的空间叫cross size

### 容器的属性

* flex-direction：决定主轴的方向(即项目排列的方向)
* flex-wrap：定义了如果一条轴线上排列不下项目，应该如何换行
* flex-flow：是flex-direction和flex-wrap属性的简写形式，默认值为row nowrap
* justify-content：定义了项目在主轴上的对齐方式，对齐方式与轴的方向有关
* align-items：定义了项目在交叉轴上如何对齐，对齐方式与交叉轴的方向有关
* align-content：定义了多根轴线的对齐方式，如果项目只有一根轴线则不起作用

```css
.box{
	flex-direction: row|row-reverse|column|column-reverse;
	/* 
	row(默认值):主轴为水平方向,起点在左端
	row-reverse:主轴为水平方向,起点在右端
	column:主轴为垂直方向,起点在上沿
	column-reverse:主轴为垂直方向,起点在下沿
	*/
	flex-wrap: nowrap|wrap|wrap-reverse;
	/*
	nowrap(默认值):默认不换行
	wrap:换行,第一行在上方
	wrap-reverse:换行,第一行在下方
	*/
	flex-flow: <flex-direction>||<flex-wrap>;
	/* 简写属性 */
	justify-content: flex-start|flex-end|center|space-between|space-around;
	/*
	flex-start(默认值):左对齐
	flex-end:右对齐
	center:居中
	space-between:两端对齐,项目之间的间隔都相等
	space-around:每个项目两侧的间隔相等.所以项目之间的间隔比项目与边框的间隔大一倍
	*/
	align-items: flex-start|flex-end|center|baseline|stretch;
	/*
	flex-start:交叉轴的起点对齐
	flex-end:交叉轴的终点对齐
	center:交叉轴的中点对齐
	baseline:交叉轴的第一行文字的基线对齐
	stretch(默认值):如果项目未设置高度或设为auto,将占满整个容器的高度
	*/
	align-content: flex-start|flex-end|center|space-between|space-around|stretch;
	/*
	flex-start:与交叉轴的起点对齐
	flex-end:与交叉轴的终点对齐
	center:与交叉轴的中点对齐
	space-between:与交叉轴两端对齐，轴线之间的间隔平均分布
	space-around:每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍
	strentch(默认值):轴线占满整个交叉轴
	*/
}
```

### 项目的属性

* order：定义项目的排序书序数值越小，排列越靠前
* flex-grow：定义项目的放大比例，默认为0，即如果存在剩余空间也不放大
* flex-shrink：定义了项目的缩小比例，默认值为1，即空间不足，该项目将缩小
* flex-basis：在分配多余空间之前，项目占据的主轴空间，浏览器将根据这个属性计算主轴是否有多余的空间。默认值为auto，即项目的本来大小。可以和width,height设置同样的值，则项目占据固定空间
* flex：是flex-grow,flex-shrink,flex-basis属性的简写，默认值为0 1 auto。后两个属性可选。有两个快捷值auto(1 1 auto)，none(0 0 auto)。建议优先使用该属性
* align-self：允许单个项目与其他项目有不一样的对齐方式，可覆盖align-items属性，默认为auto，表示继承父元素的align-items属性，如果没有父元素等他有stretch

```css
.item{
	order: <integer>;
	flex-grow: <number>; /* default 0 */
	flex-shrink: <number>; /* default 1 */
	flex-basis: <length> | auto; /* default auto */
	flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
	align-self: auto | flex-start | flex-end | center | baseline | stretch;	
}
```

## 常见问题

* flex:1    flex-grow,flex-shrink取1，flex-basis取0%。内容区则会自动放大占满剩余空间。定义了成员项可以占用容器中剩余空间的大小。如果所有的成员项设置相同的值flex:1，他们将平均分配剩余空间，如果一个成员项的值为flex:2，其他成员项设置的值为flex:1，那么这个成员项所占用的剩余空间是其他成员的两倍
* 

