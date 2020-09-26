# CSS

## 关于CSS3新增的特性

* 边框：
  * border-radius:圆角边框
  * border-shadow:矩形阴影
  * border-image图片边框

* 动画：@keyframes
* 2D转换：
  * translate()
  * rotate()
  * scale()
* 文本效果：
  * text-shdow



---



## 盒子模型

是用来装页面元素的矩形区域；css3中引入了box-sizing属性，值为content-box为标准盒模型；值为border-box指IE盒模型

* 标准盒子模型：width，height指content部分的宽高度
* IE盒模型：width，height指content+padding+border的宽高度

### margin，padding，border

* padding：在元素内容的一边或多个边添加空间，它是透明的，所以元素的背景颜色或背景图像会显示出来
* border：控制元素每个边的边框显示，包括内容和padding，这一般是一条着色或透明的线条，border属性定义了该线条的宽度，线型和颜色，可以是圆角甚至是边框图像，边框在元素padding和margin之间添加，默认会覆盖元素的背景
* margin：影响元素的一边或多个边上的空间，且是透明的；但与padding不同，它可以是负值和auto值，这些允许将元素从最初的位置移开，或者改变它与周围元素的交互方式











## CSS选择器

### 选择器的权重值

若选择器的权重一致则选取后面的样式

* !important：最高优先级

* 内联样式：1000
* ID选择器：100
* 类选择器，属性选择器，伪类选择器：10
* 类型选择器，伪元素：1

---

### 选择器

#### 组合选择器

* 后继选择器：可以选择出一个元素中某种元素类型的所有实例`article p{...}`
* 子组合器：选择父元素中的直接子元素`article > p{...}`
* 临近同级选择器：选择文档中彼此相邻并且有相同的父元素`h2 + p{...}`
* 一般同级选择器：第二个选择器不必要跟在第一个选择器后面但两者仍有相同父元素`h3 ~ ul{...}`

#### 伪类选择器

例：`a:hover{color:red;}`

* :link 表示普通的链接
* :visted 表示访问过的链接
* :hover 表示鼠标移入的状态
* :active 表示超链接被点击状态
* :focus 获取焦点
* ::selection 选中内容使用的样式

#### UI元素伪类选择器

* :disable 禁用的
* :checked 选中的
* :enable 启用的

#### Target伪类

选中的元素称为链接的活动目标，也就是说为跳转的目标设置样式

* :target

#### 结构伪类

* :first-child 允许在文档树中选择给定元素的第一个子元素 `div p:first-child{...}`
* :last-child 选择最后一个子元素 `nav li:last-child{...}`
* :nth-child 允许选择给定父元素的一个或多个特定的子元素，它可以将数字(整数)，关键词(odd(奇数)或even(偶数))，或表达式作为参数 `tr:nth-child(4n+1) td{...}`  从第一行开始每隔三行添加样式
* :nth-last-child 与:nth-child基本相同，但从最后最后一个元素开始计数 `tr:nth-last-child(-n+5) td{...}`  给后五行设置样式
* :only-child 选出父元素的唯一子元素，若一个动态生成的列表只包含一项，使用它就很方便 `ul li:only-child{...}`
* :first-of-type 工作方式与子选择器相同，区别是类型伪类只选择与应用了选择器的元素相同类型的元素。不能保证没有不同的子元素时，就可以使用类型伪类
* :last-of-type
* :nth-of-type 工作方式与nth-child相同，使用语法也相同，若在要选择的元素之间有其他元素，使用它更有效
* :nth-last-of-type 可以从最后一项向前数
* :only-of-type 选择父元素中的子元素，在该父元素中，没有该类型的其他子元素
* :empty 表示没有内容的元素
* :root  选择html元素

#### 子串选择器

* Start  with子串选择器  ^   `a[href^="http://"]{...}`
* ends with子串选择器  $  `a[href$=".pdf"]{...}`
* Contains子串选择器  *  `a[href*="twitter"]{...}`

#### 伪元素

* ::first-letter
* ::first-line
* ::before  用于在元素的内容(或另一个伪元素)之前生成的内容
* ::after  用于在元素的内容(或另一个伪元素)之后生成的内容

#### 属性选择器

* [属性名]：选取含有指定属性的元素  `a[target] {...}`
* [属性名=“属性值”]
* [属性名$=“属性值”]
* [属性名^=“属性值”]
* [属性名*=“属性值”]

#### 否定伪类

:not `input:not([type="submit"]){...}`  给不是submit按钮的所有窗体设置输入样式

#### 特性

* required特性 `input[required]{...}`  指定需要的字段
* =  `input[type="checkbox"]{...}`
* ~ `a[rel~="license"]{...}`  从用空格分隔的值列表中选择特定的特行值
* | `a[hreflang|="en"]{...}`  允许在带连字符的列表中选择以特定值开头的元素











---



## position属性

* 固定定位fixed
  	
   * 元素的位置相对于浏览器是固定位置，即使窗口是滚动的它也不会移动
   * fixed定位使元素的位置与文档流无关，因此不占据空间
   
   * fixed定位的元素和其他元素重叠
   * 带position:fixed的元素最初也出现在静态位置上，但top,right,bottom,left会相对于视口来定位他
   
* 相对定位relative
  	
   * 带position:relative的方框占用的空间可以使用top,right,bottom,left相对于这个位置移动方框
   * 如果对一个元素进行相对定位，它将出现在它所出现的位置上。然后可以通过设置垂直或水平位置，让这个元素相对于它的起点进行移动。
   * 在使用相对定位时，无论是否进行移动，元素仍然占据原来的空间，因此移动元素会导致覆盖其他框
   
*  绝对定位absolute
    	
     * 如果没有设置width，它的宽度会缩小为内容的宽度
     * 绝对定位的元素的位置相对于已定位的父元素，如果元素没有已定位的父元素，那么它的位置相对于\<html\>
     * absolute定位使元素的位置与文档流无关，因此不占据空间
     * absolute定位的元素和其他元素重叠
     
*  粘性定位sticky
    	
    	* 元素先按照普通文档流定位，然后相对于该元素在流中的(BFC)和最近的块级祖先元素定位。而后，元素定位表现在跨域特定阈值前为相对定位，之后为固定定位
    
*  默认定位static
    	
  * 默认值，没有定位，元素出现在正常的流中
  * inherit：规定应该从父元素继承position属性的值









## 响应式布局

### css中的单位

* px：像素
* em：1em为字体当前尺寸，2em为字体尺寸的两倍、
* ex：一个ex是一个字体的x-height(x-height通常是字体尺寸的一般)
* %：百分比
* rem：相对与根节点html的字体大小来计算
* vw：视窗宽度：1vw等于视窗宽度的1%
* vh：视窗高度：1vh等于视窗高度的1%

### 关于响应式布局的几种方式

* 媒体查询：针对不同媒体类型定义不同的样式，当重置浏览器窗口大小的过程中，页面会根据浏览器的宽度和高度重新渲染页面。

  * 他会根据屏幕增大或减小的时候，后面的样式会覆盖前面的样式，因此移动端优先使用min-width，PC端优先使用max-width

    ```css
    /*移动端优先*/
    /* iphone6 7 8 */
    body {
        background-color: yellow;
    }
    /* iphone 5 */
    @media screen and (max-width: 320px) {
        body {
          background-color: red;
        }
    }
    /* iphoneX */
    @media screen and (min-width: 375px) and (-webkit-device-pixel-ratio: 3) {
        body {
          background-color: #0FF000;
        }
    }
    /* iphone6 7 8 plus */
    @media screen and (min-width: 414px) {
        body {
          background-color: blue;
        }
    }
    /* ipad */
    @media screen and (min-width: 768px) {
        body {
          background-color: green;
        }
    }
    /* ipad pro */
    @media screen and (min-width: 1024px) {
        body {
          background-color: #FF00FF;
        }
    }
    /* pc */
    @media screen and (min-width: 1100px) {
        body {
          background-color: black;
        }
    }
    
    ```

    ```css
    /*PC端优先*/
    /* pc width > 1024px */
        body {
            background-color: yellow;
        }
    /* ipad pro */
    @media screen and (max-width: 1024px) {
        body {
            background-color: #FF00FF;
        }
    }
    /* ipad */
    @media screen and (max-width: 768px) {
        body {
            background-color: green;
        }
    }
    /* iphone6 7 8 plus */
    @media screen and (max-width: 414px) {
        body {
            background-color: blue;
        }
    }
    /* iphoneX */
    @media screen and (max-width: 375px) and (-webkit-device-pixel-ratio: 3) {
        body {
            background-color: #0FF000;
        }
    }
    /* iphone6 7 8 */
    @media screen and (max-width: 375px) and (-webkit-device-pixel-ratio: 2) {
        body {
            background-color: #0FF000;
        }
    }
    /* iphone5 */
    @media screen and (max-width: 320px) {
        body {
            background-color: #0FF000;
        }
    }
    ```

* 百分比布局：可以使浏览器中的组件的宽高随着浏览器的高度的变化而变化。CSS支持最大最小高，可以将百分比和max/min一起结合使用来定义元素在不同设备下的宽高

  ```css
  /* iphone6 7 8 */
  @media screen and (max-width: 375px) and (-webkit-device-pixel-ratio: 2) {
      aside {
        float: none;
        width: 100%;
        height: 3%;
        background-color: black;
      }
      main {
        height: calc(100vh - 3%);
        background-color: red;
      }
  }
  ```

  * 子元素的`height`或`width`中使用百分比，是相对于子元素的直接父元素，`width`相对于父元素的`width`，`height`相对于父元素的`height`；子元素的`top`和`bottom`如果设置百分比，则相对于直接非`static`定位(默认定位)的父元素的高度，同样子元素的`left`和`right`如果设置百分比，则相对于直接非`static`定位(默认定位的)父元素的宽度；子元素的`padding`如果设置百分比，不论是垂直方向或者是水平方向，都相对于直接父亲元素的`width`，而与父元素的`height`无关。跟`padding`一样，`margin`也是如此，子元素的`margin`如果设置成百分比，不论是垂直方向还是水平方向，都相对于直接父元素的`width`；`border-radius`不一样，如果设置`border-radius`为百分比，则是相对于自身的宽度，除了`border-radius`外，还有比如`translate`、`background-size`等都是相对于自身的；

  * 缺点：计算困难，如果要定义一个元素的宽度和高度，按照设计稿需要换算成百分比的；各种属性相对的父元素不一定一致

* rem布局：rem是相对于根元素html的font-size来决定大小，根元素的font-size相当于提供了一个基准，当页面的size发生变化时，只要改变font-size的值，那么以rem为固定单位的元素的大小也会发生响应的变化。因此通过rem实现相应式布局，只需根据视图容器的大小动态改变font-size

  ```js
  var docEl = document.documentElement;
  var resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize';
  function recalc(){
      var clientWidth = docEl.clientWidth;
      if(!clientWidth){ return docEl.style.fontSize = 100 * (clientWidth / 750)+'px' }
  }
  window.addEventListener(resizeEvt,recalc,false);
  ```

  * 思路：

    * 一般不给元素设置具体的宽度，对于一些小图标可以设定具体宽度只
    * 高度值可以设置固定值
    * 所有设置的固定值都用rem做单位，在HTML总设置一个基准值：`px`和`rem`的对应比例，然后在效果图上获取`px`值，布局的时候转化为`rem`值
    * js获取真实屏幕的宽度，让其除以设计稿的宽度，算出比例，把之前的基准值按照比例进行重新的设定，这样项目就可以在移动端自适应了

  * 缺点：需要引入改变font-size大小的js代码

* 视口单位：vw/vh/vmin/vmax。用视口单位度量，视口宽度为100vw，视口高度为100vh

  * 与%区别：
    * %大部分相对于祖先元素，也有相对于自身的情况
    * vw/vh相对于视窗的尺寸

* 图片响应式：大小自适应：能够保证图片在不同的屏幕分辩率下出现拉伸，压缩的情况；根据不同的屏幕分辨率和设备像素来尽可能选择对应分辨率的图片，这样在小屏幕上就不用使用高清图可以减少网络带宽

  * max-width：图片随着容器大小进行缩放

    ```css
    img {
        display: inline-block;
        max-width: 100%;
        height: auto;
    }
    ```

    * `inline-block` 元素相对于它周围的内容以内联形式呈现，但与内联不同的是，这种情况下我们可以设置宽度和高度。

    * `max-width`保证了图片能够随着容器的进行等宽扩充（即保证所有图片最大显示为其自身的 100%

    * `height`为`auto`可以保证图片进行等比缩放而不至于失真。如果是背景图片的话要灵活运用`background-size`属性。

  * srcset

    ```css
    <img srcset="photo_w350.jpg 1x, photo_w640.jpg 2x" src="photo_w350.jpg" alt="">
    ```

    * 如果屏幕的dpi = 1的话则加载1倍图，而dpi = 2则加载2倍图，手机和mac基本上dpi都达到了2以上，这样子对于普通屏幕来说不会浪费流量，而对于视网膜屏来说又有高清的体验；如果浏览器不支持`srcset`，则默认加载src里面的图片

    * 缺点：有时会加载srcset与src两张图片

      * 解决方法：使用picture标签，picture中可包含source标签对图片进行兼容性处理

### 响应式布局常见解决方案

* 基础概念：
  * 像素：是网页布局的基础，一个像素表示了计算机屏幕所能显示的最小区域，像素分为css像素和物理像素。在js或css代码中使用的px单位就是css像素，物理像素也称设备像素，只与设备的硬件密度相关，任何设备的物理像素都是固定的
  * 视口：只浏览器显示内容的屏幕区域
    * 布局视口
      * 布局视口定义了pc网页在移动端的默认布局行为，也就是说在不设置网页的viewport的情况下，pc端的网页默认会以布局视口为基准，在移动端进行展示
    * 视觉视口
      * 视觉视口表示浏览器内看到的网站的显示区域，用户可以通过缩放来查看网页的显示内容，从而改变视觉视口。
    * 理想视口
      * 在移动设备中就是指设备的分辨率。换句话说，理想视口或者说分辨率就是给定设备物理像素的情况下，最佳的“布局视口”。

* px和视口
  * 1个css像素可以表示为物理像素/分辨率，如在iphone6移动端一个css像素为0.75px而在pc端则为2px
* 媒体查询
  * 在css文件中，1px所表示的物理像素的大小是不同的，因此通过一套样式，是无法实现各端的自适应，所以给每一种设备设置一套不同的样式来实现自适应效果

```css
@media screen and (max-width: 960px){
    body{
      background-color:#FF6699
    }
}

@media screen and (max-width: 768px){
    body{
      background-color:#00FF66;
    }
}
```

缺点：在浏览器大小改变时，需要改变的样式太多，那么多套样式代码会很繁琐

* 百分比
  * 子元素height和width的百分比：子元素的height或width中使用百分比，是相对于子元素的直接父元素，width相对于父元素的width，height相对于父元素的height。
  * top和bottom 、left和right：子元素的top和bottom如果设置百分比，则相对于直接非static定位(默认定位)的父元素的高度，同样，子元素的left和right如果设置百分比，则相对于直接非static定位(默认定位的)父元素的宽度
  * padding：子元素的padding如果设置百分比，不论是垂直方向或者是水平方向，都相对于直接父亲元素的width，而与父元素的height无关。子元素的初始宽高为0，通过padding可以将父元素撑大，说明padding不论宽高，如果设置成百分比都相对于父元素的width
  * margin：跟padding一样，margin也是如此，子元素的margin如果设置成百分比，不论是垂直方向还是水平方向，都相对于直接父元素的width。
  * border-radius：border-radius不一样，如果设置border-radius为百分比，则是相对于自身的宽度
  * 缺点：
    * 计算困难，如果我们要定义一个元素的宽度和高度，按照设计稿，必须换算成百分比单位
    * 各个属性中如果使用百分比，相对父元素的属性并不是唯一的

* 通过rem来实现响应式布局
  * rem单位都是相对于根元素html的font-size来决定大小的,根元素的font-size相当于提供了一个基准，当页面的size发生变化时，只需要改变font-size的值，那么以rem为固定单位的元素的大小也会发生响应的变化。如果通过rem来实现响应式的布局，只需要根据视图容器的大小，动态的改变font-size即可
  * 可通过webpack实现一些单位之间的转换
  * 缺点：在响应式布局中，必须通过js来动态控制根元素font-size的大小，具有一定的耦合性，且font-size的代码要放在样式之前
* 通过vw/vh实现自适应
  * vw表示相对于视图窗口的宽度，vh表示相对于视图窗口高度，vmin表示vw和vh中的较小值，vmax表示vw和vh中的较大值
  * 单位换算：如果要将px换算成vw单位，很简单，只要确定视图的窗口大小



---



## block、inline、inline-block的区别。

block元素会独占一行，多个block元素会各自新起一行。默认情况下，block元素宽度自动填满其父元素宽度。

block元素可以设置width,height属性。块级元素即使设置了宽度,仍然是独占一行。

block元素可以设置margin和padding属性。



inline元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行，其宽度随元素的内容而变化。

inline元素设置width,height属性无效。

inline元素的margin和padding属性，水平方向的padding-left, padding-right, margin-left, margin-right都产生边距效果；但竖直方向的padding-top, padding-bottom, margin-top, margin-bottom不会产生边距效果。



inline-block：简单来说就是将对象呈现为inline对象，但是对象的内容作为block对象呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个link（a元素）inline-block属性值，使其既具有block的宽度高度特性又具有inline的同行特性



---



## clientHeight,scrollHeight,offsetHeight ,scrollTop, offsetTop,clientTop

* clientHeight：表示的是可视区域的高度，不包含border和滚动条

  offsetHeight：表示可视区域的高度，包含了border和滚动条

  scrollHeight：表示了所有区域的高度，包含了因为滚动被隐藏的部分。

  clientTop：表示边框border的厚度，在未指定的情况下一般为0

  scrollTop：滚动后被隐藏的高度，获取对象相对于由offsetParent属性指定的父坐标(css定位的元素或body元素)距离顶端的高度。



---



##  元素居中方案

### 水平居中

父元素相对定位，子元素绝对定位

* `top:0;right:0;bottom:0;left:0;`     `margin:auto;`

* `top:30%;left:50%`      `margin-top,margin-left的值减去自身的一半`

* display:inline的属性可以设置text-align来实现

### 垂直居中

* 父元素display:flex,align-items:center
* 父元素绝对定位top:50%,margin-top:-(height/2)
* 高度不确定用transform:translateY(-50%)
* 父元素table布局，子元素设置vertical-align:center



### 容器内居中

* position:absolute;left:50%;top:50%;transform:translate(-50%,-50%)
* 将父元素设置成display:table,子元素设置为单元格display:table-cell
* 父元素固定宽高，利用定位及设置子元素margin值为自身的一半
* 父元素固定宽高，子元素设置position:absolute,margin:auto平均分配margin



---



### BFC

块级格式化上下文，是一个独立的渲染区域，规定了内部如何布局，并且这个区域的子元素不会影响到外面的元素。

满足以下条件即可触发BFC：

* 根元素，即html元素
* float的值不为none
* overflow的值不为visible
* position为fixed或absolute的元素
* display为inline-block,flex.inline-flex,table-cell,table-caption

作用特性：

* 阻止垂直外边距折叠

* 清除内容较多时对浮动元素的环绕
* 为父元素创建一个BFC改变元素内容较少时出现的高度塌陷

当元素设置了overflow样式且值为visible时，该元素就构建了一个BFC，BFC在计算高度时，内部浮动元素的高度也要计算在内，也就是说技术BFC区域内只有一个浮动元素，BFC的高度也不会发生塌缩，所以达到了清除浮动的目的



---



## 关于浮动



### 清除浮动

* 使用带clear属性的空元素
* 使用CSS的overflow属性：给浮动元素的容器添加overflow:hidden;或overflow:auto;可以清除浮动。另外在IE6中还需要触发hasLayout,例如为父元素设置容器宽高或设置zoom:1
* 给浮动的元素容器添加浮动：给浮动元素的容器也添加上浮动属性即可清除内部浮动，但是这样会使其整体浮动，影响布局，不推荐使用
* 使用邻元素处理：给浮动元素后面的元素添加clear属性
* 使用CSS的:after伪元素：给浮动元素的容器添加一个clearfix的class，然后给这个class添加一个:after伪元素实现元素末尾添加一个看不见的块元素清除浮动







### 让元素消失的方案

* display:none改变布局，类似于删除了该元素
* visibility:hidden不会改变布局，不会触发绑定事件
* opacity:0不会改变页面布局，能触发点击事件





## 设置一个元素的背景颜色，背景颜色会填充哪些区域

background-color设置的背景颜色会填充元素的content,padding,border区域



## 实现圆形可点击区域

1.客户端图像映射，带有可点击区域的一幅图像

2.css实现

3.JavaScript方法定义一个圆形的区域

## 实现0.5px的细线

* 使用meta viewport的方法

```css
<meta name="viewport" content="width=device-width, initial-scale=0.5, minimum-scale=0.5, maximum-scale=0.5"/>
```

只针对移动端

* transform:scale(0.5,0.5)

## css3动画与js动画对比

css3动画：@keyframes 规则用于创建动画，使用from...to或百分比来控制动画；animation属性为动画添加其他效果，比如animation-delay,animation-duration,animation-direction等；也可以使用transform进行一些动画变换

* js动画
  * 缺点：
    * 在浏览器主线程中运行，主线程还有其他js脚本，样式布局之类的，可能会对其干扰导致动画出现阻塞从而造成丢帧的现象
    * 复杂度比较高
  * 优点：
    * 控制动画的能力比较强，可以在播放过程中进行控制使其开始暂停
    * 动画效果比较丰富比如曲线运动
    * css有兼容性问题，js比较少
* css动画
  * 主要分为transition和animation
    * transition需要触发一个事件才能改变属性，from...to两帧执行一次
    * animation不需要触发任何事件的情况下可以随时间改变属性值，每帧执行
  * 缺点：
    * 运行过程比较弱，不能再特定位置添加一个特定的事件点
    * 代码冗长
  * 优点：
    * 浏览器可以对动画进行优化，会把每一次重绘的步骤合并起来减少消耗，也可以通过硬件gpu来提高性
    * js在主线程执行，css订花可以使用合成器线程执行





---



### link与@import的区别

* link属于html标签没有兼容性，@import是css提供的只要IE5以上才能识别
* link的权重值高于import
* link会在页面被加载的时候同时被加载；@import所引用的css会等到页面加载结束后加载



### 为什么img元素时inline还可以设置宽高

因为img是一个可替换元素拥有内置宽高，类似的元素还有video，iframe等。css可以影响可替换元素的位置，但不会影响到可替换元素自身的内容

### 关于文本溢出的处理

text-overflow属性，值为clip是修剪文本，ellipsis为显示省略符号来表示被修剪的文本，string为使用给定的字符串来代表被修剪的文本

### css3新增的calc属性

动态计算长度值，运算符前后需要保留一个空格

`width:calc(100% - 10px)`









### 重绘与重排

* document.write：重排整个页面；innerHTML：重绘页面的一部分
* 浏览器的运行机制：
  * 构建DOM树：渲染引擎解析html文档，首先将标签转换成DOM树中的DOM节点(包括js生成的标签)生成内容树
  * 构建渲染树：解析对应的css样式文件，以及html中可见的指令，比如b标签之类的，构建渲染树
  * 布局渲染树：从根节点递归调用，计算每一个元素的大小位置，给出每个节点所应该在屏幕上出现的精确位置
  * 绘制渲染树：遍历渲染树，绘制每个节点

**重绘：**当盒子的位置，大小以及其他属性(比如颜色，字体大小)都确定下来之后，浏览器把这些原色都按照各自的特性绘制一遍，将内容呈现在页面上。重绘是指一个元素外观的改变所触发的浏览器行为，浏览器会根据元素的新属性重新绘制，使元素呈现新的外观。触发重绘的条件：改变元素的外观属性如color,background-color等

**重排：**当渲染树中的一部分或全部因为元素的规模尺寸，布局，隐藏等改变而需要重新构建，这就是重排。每个页面至少需要一次重排，就是在页面第一次加载的时候

**两者关系：**在重排的时候，浏览器会使渲染树中受到影响的部分失效，并重新构造这部分渲染树。完成回流后，浏览器重新绘制受影响的部分到屏幕中，这个过程就是重绘。也就是说重排必定会引发重绘，重绘不一定会引发重排。

**重排的条件：**页面初始渲染；添加或删除可见的DOM元素；元素位置改变或使用动画；元素尺寸的改变;浏览器窗口尺寸的变化(触发resize事件)；填充内容的改变；读取某些元素属性等等

**优化：**

* 浏览器方面的优化：会自动把会引起重绘与重排的操作放入一个队列，等到达一定数量或一定时间间隔，对这些操作进行一个批处理
* 其他优化：减少对渲染树的操作，合并多次的DOM和样式修改
  * 直接改变元素的calssName
  * 先设置元素为display:none，然后进行页面布局等操作，设置完成后将元素设置为display:block，这样只会引发两次重绘与重排
  * 将需要多次重排的元素，position属性设为absolute或fixed，元素脱离了文档流，它的变化不会影响到其他元素









# CSS样式实现

## 背景与边框

### 半透明边框

通过rgba设置一个border的值为透明色，背景色会从透明处透出从而破坏布局颜色，可以使用background-clip：paddding-box

初始值为border-box，意味着背景会被元素的border box裁减掉，如果不希望背景入侵边框所在的范围，就要设为padding box



---







## 形状

### 自适应椭圆

给任何正方形元素设置一个足够大的border-radius可以把它变成一个圆形

border-radius可以单独指定水平和垂直半径，只要用一个`/` 分隔即可，只要把它圆角的两个半径值指定为元素宽高的一般就能得到一个精确的椭圆

但是存在缺陷，当元素尺寸发生变化时，border-radius的值也要发生修改，所以可以用百分比设置为50%

半椭圆和四分之一椭圆按照顺时针设置每个角的属性，平角为0，圆角为100%；

```css
自适应椭圆
.div{
    border-radius: 50%;
}
半椭圆
.div{
    border-radius: 100% 0 0 100% / 50%;
}
四分之一椭圆
.div{
    border-radius: 100% 0 0 0
}
```

---

### 平行四边形实现

* 通过使用skew()对矩形进行斜向拉伸：会导致它的内容也发生斜向变形；
  * 解决方法，使用额外的元素包裹然后对内容进行反向斜向拉伸

```css
.div{
    transform:skewX(-45deg)
}
```

* 把所有样式应用到伪元素上然后对伪元素进行变形，因为内容不是包含在伪元素里面所以不会受到变形的影响；要使伪元素保持灵活性自动继承宿主元素的尺寸，或者当宿主元素的尺寸是由其内容来决定的时候，可以使用相对定位和绝对定位，然后把所有偏移量都设置为0，这样在水平和垂直元素上都会被拉伸至宿主元素的尺寸

```css
.button{
	position: relative;
}
.button::before{
	content: '';
	position: absolute;
	top: 0;right: 0;bottom: 0;left: 0;
}
/* 此时伪元素生成的方块是重叠在内容之上的,一旦给它设置背景就会遮住内容,可以通过设置z-index将他的堆叠元素推到宿主元素之后 */
.button{
	position: relative;
}
.button::before{
	content: ''; /*用伪元素来生成一个矩形*/
	position: absolute;
	top: 0;right: 0;bottom: 0;left: 0;
	background-color: #58a;
	transform: skew(45deg);
}
/* 设置样式为正方形使用rotate后还可以得到菱形元素 */
```

关键在于利用伪元素以及定位属性产生了一个方块，然后对伪元素进行样式设置然后将其放在宿主元素的下层

---

### 菱形图片的实现

将一个div标签包裹起来使用rotate变换样式，但是会因为裁剪问题变成一个八角的形状。这时可以使用scale将图片放大，因为通过width属性只会基于左上角进行放大

可以使用clip-path属性对元素进行裁剪