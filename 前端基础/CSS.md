# CSS

### 关于CSS3新增的特性

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





## css中的单位

* px：像素
* em：1em为字体当前尺寸，2em为字体尺寸的两倍、
* ex：一个ex是一个字体的x-height(x-height通常是字体尺寸的一般)
* %：百分比
* rem：相对与根节点html的字体大小来计算
* vw：视窗宽度：1vw等于视窗宽度的1%
* vh：视窗高度：1vh等于视窗高度的1%

## CSS选择器

* 元素选择器

  * 通常是某个html元素，甚至可以是html本身

  * ```css
    html {color:black;}
    ```

* 类选择器

  * 将选择器与元素关联，需要在元素中添加class属性，然后通过.属性名来使用选择器

* ID选择器

  * 在元素中添加id属性，通过#s属性名来使用选择器

* 选择器分组

  * 可以将任意多个元素选择器使用逗号隔开，形成选择器分组，一次来使用多个选择器

* 后代选择器

  * 对元素内的元素进行选择，通过父元素 子元素的形式进行选择，特点是无论嵌套层数有多少都可以确认选择出该父元素下的所有匹配的后代元素

  * ```css
    h1 em {color:red;}
    选择的是h1中的所有em元素
    ```

* 子元素选择器

  * 相比于后代选择器，子元素选择器只选择某个元素的第一个匹配子元素。也无法做出嵌套下的选择.但是如果有两个对应的父元素下的第一子元素，则两个都会被选择。

  * ```css
    h1 > p{color:red}
    ```

* 相邻兄弟选择器

  * 选择紧接在另一个元素后的元素，而且两者有相同的父元素。比如同一父元素下的h1元素和p元素

  * ```css
    h1 + p {margin-top:50px;}
    ```

* 伪类

  * 锚伪类
    * a:link    未访问的链接
    * a:visited    已访问的链接
    * a:hover    鼠标在连接上悬停
    * a:active    选定的链接 
  * :first-child：选择元素的第一个子元素

* 伪元素

  

* css3选择器

  

  ​	

## import

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

### block、inline、inline-block的区别。

block元素会独占一行，多个block元素会各自新起一行。默认情况下，block元素宽度自动填满其父元素宽度。

block元素可以设置width,height属性。块级元素即使设置了宽度,仍然是独占一行。

block元素可以设置margin和padding属性。



inline元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行，其宽度随元素的内容而变化。

inline元素设置width,height属性无效。

inline元素的margin和padding属性，水平方向的padding-left, padding-right, margin-left, margin-right都产生边距效果；但竖直方向的padding-top, padding-bottom, margin-top, margin-bottom不会产生边距效果。



inline-block：简单来说就是将对象呈现为inline对象，但是对象的内容作为block对象呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个link（a元素）inline-block属性值，使其既具有block的宽度高度特性又具有inline的同行特性









# CSS

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

