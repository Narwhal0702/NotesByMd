# jQuery

## 基本内容

$就是jQuery的一个简写

```js
$(document).ready(function(){});
$(document).ready(function(){});
jQuery(document).ready(function(){});
jQuery(function(){});
$(function(){});  //推荐写法
```

与window.onload区别：window.onload必须等网页中所有内容加载完毕后才能执行，不能同时编写多个；$(function(){})在网页中所有DOM元素结构绘制完毕后就执行，可能DOM元素关联的东西没有加载完，可以编写多个

在jQuery对象中无法使用DOM对象的任何方法

**变量命名：**var $variable = jQuery对象;    var variable = DOM对象;

**jQuery对象转DOM对象：**[index]和get(index)；jQuery对象是一个数组对象，可以通过[index]的方法得到相应的DOM对象，或通过jQuery本身提供的get(index)方法得到相应的DOM对象

```js
var $cr = $("#cr");
var cr = $cr[0];
var cr = $cr.get(0);
```

**DOM对象转jQuery对象：**只需要用$()把DOM对象包装起来，就可以获得一个jQuery对象

```js
var cr = document.getElementById("cr");
var $cr = $(cr)
```

#### 关于jQuery库与其他库的冲突：

* jQuery在其他库之后导入
  * 调用jQuery.noConflict()函数将变量$的控制权移交给其他JavaScript库
  * 可以自定义一个快捷方式

  ```js
  jQuery.noConflict();
  var $j = jQuery.noConflict();
  ```

  * 其他方法：

  ```js
  jQuery.noConflict();
  //使用jQuery设定页面加载时执行的函数
  jQuery(function($){})
  //定义匿名函数并设置形参为$,匿名函数内部的$均为jQuery
  (function($){})(jQuery)
  ```

* jQuery库在其他库之前导入
  
  * 可以直接用"jQuery"来做jQuery的工作，同时可以使用$()方法作为其他库的快捷方式

## 选择器

可以非常便捷和快速地找出特定的DOM元素，然后为他们添加对应的行为

## DOM操作

利用jQuery选择器查到需要的元素后，可以使用attr()方法来获取它的各种属性。

```js
//创建元素节点
var $li_1 = $("<li></li>")
//插入到文档
$("ul").append($li_1);
//创建文本节点->在创建元素节点时直接把文本内容写出来
var $li_1 = $("<li>content</li>")
//创建属性节点->创建元素节点时一起创建
var $li_1 = $("<li title="test">content</li>")
```

#### 节点操作

 插入节点，删除节点，复制节点，替换节点，包裹节点

#### 属性操作

获取属性，设置属性，删除属性

#### 样式操作

获取样式，设置样式，追加样式，移除样式，切换样式

#### CSS-DOM

offset()，position()，scrollTop()，scrollLeft()

## 事件和动画

在jQuery方法内注册的事件，只要DOM就绪就会被执行，因此可能此时元素的关联文件未下载完，所以图片的宽高属性此时不一定有效，可以使用load方法解决

```js
$(window).load(function(){})
```

#### 事件绑定

bind( type [, data] , fn )：第一个参数是事件类型；第二个参数为可选参数，作为event.data属性值传递给事件对象的额外数据对象；第三个参数用来绑定处理函数。可以使用简写方式。

#### 合成事件

hover(enter,leave)：用于模拟光标悬停，当光标移动到元素上时，会触发第一个函数，移出时会触发第二个函数

toggle(fn1,fn2,fn3)：用于模拟鼠标连续点击事件，第一次单机触发第一个函数，再次单机同一元素时触发指定的第二个函数

#### 事件冒泡，默认行为，事件捕获

事件冒泡解决方式：

* 事件对象：为函数添加一个event参数，这样单机元素时，事件对象就被创建了。这个事件对象只有事件处理函数才能访问到，事件函数执行完毕后事件对象就被销毁
* 停止事件冒泡：event.stopPropagation()
* return false

阻止默认行为：

* preventDefault()
* return false

事件捕获：jQuery不支持事件捕获

#### 事件对象的属性

```js
event.type()
event.preventDefault()
event.stopPropagation()
event.target()	获取到触发事件的元素
event.relatedTarget()
event.pageX()
event.pageY()
event.which()
event.metaKey()
event.originalEvent()
```

#### 移除事件

## 动画

**show()方法和hide()方法：**会修改元素的display样式，hide()在修改内容的display值时，会记住原先display的属性值；如果需要显示动画可以加一个速度参数。

**fadeIn()方法和fadeOut()方法：**改变元素的透明度实现淡入淡出效果

**slideUp()方法和slideDown()方法：**会改变元素的高度，如果一个元素的display属性值为none，调用slideDown()方法时，元素会由上至下衍生显示，slideUp()方法正好相反，元素将由下到上缩短隐藏

**animate(params,speed,callback)：**params一个包含样式属性及值的映射；speed速度参数，可选；callback在动画完成时执行的函数，可选

**stop([clearQueue],[gotoEnd])：**clearQueue代表是否要清空为执行完的动画队列，gotoEnd代表是否直接将正在执行的动画跳转带结束状态

## 表单，表格





### 核心函数$()

作用：调用jQuery的核心函数

```js
$(function(){});  //接收一个函数
//接收一个字符串选择器
$(function(){
    var $box1 = $(".box1");
});
//接收一个代码片段，并根据字符串代码片段创建对应的DOM元素
$(function(){
    var $p = $("<p>aaa</p>");
});
//接收一个DOM元素，将DOM元素包装成一个jQuery对象
$(function(){
    var span = document.getElementsByTagName("span")[0];
    var $span = $(span);
});
```

### 静态方法

* $map(arr,function(index,value))：相比于原生map可以遍历伪数组
* $each(arr,function(index,value))：相比于原生each可以遍历伪数组
* $trim(str)：去除字符串的首尾空格
* $.isWindow()：判断传入的对象是否为window对象
* $.isArray()：判断是否为数组，伪数组为false
* $isFunction()：判断传入对象是否为函数，传入jQuery为true，说明jQuery本质上是一个匿名函数
* $.holdReady()：暂停ready的执行

### 内容选择器

:empty    找到内容为空的，没有文本与子元素

:parent    找到有文本内容与子元素的指定元素

:contains(text)    找到包含具体内容的指定元素

:has(selector)    找到包含具体子元素的指定元素

### 属性和属性节点

属性：对象身上保存的变量

属性节点：在编写html代码时在html标签中添加的属性，保存在attributes属性中

属性节点的操作：

* element.setAttribute("attributename","value")

* element.getAttribute("attributename")

jQuery中的操作：

* attr(name|pro|key,value|function)：获取属性节点的值，传入一个元素，获取属性节点的值(无论找到多少个元素，都只会返回一个属性节点的值)；传入两个元素，设置属性节点的值(找到多少个元素就会设置多少属性节点的值，如果设置的属性节点不存在，系统自动新增)
* removeAttr(name)：删除属性节点(删除所有找到元素的属性节点，name间使用空格隔开可以删除多个属性节点)
* prop：类似于attr方法，不仅能操作属性且能操作属性节点

### 类相关方法

addClass(class|fn)：添加一个类(添加多个以空格隔开)

removeClass([class|fn])：删除一个类(删除多个以空格隔开)

toggleClass(class|fn[,sw])：切换类，有则删除，没有则添加

### 文本值相关方法

html([val|fn])

text[val|fn]

val([val|fn|arr])

### 操作css样式方法

### 尺寸和位置操作方法

offset([coorfinates])：获取元素距离窗口的偏移位，传入参数则修改

position()：获取元素距离定位元素的偏移量

.width()：有参数则设置，无参数则获取

.scrollTop()：获取滚动的偏移位，传入参数则为设置

```js
$("body").scrollTop()+$("html").scrollTop()
$("html,body").scrollTop()
```

### 事件



### 效果