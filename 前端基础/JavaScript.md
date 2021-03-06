# JavaScript数据类型


## Array类型

* 构造时可以省略new操作符
* 通过设置length属性的值可以实现向数组末尾移除项，或添加新项undefined
* api：
  * Array.isArray(value):检测某个值是不是数组
  * toString():返回数组的字符串表示，中间以逗号分隔；与toLocalString()区别，toLocalString()调用的是每一项的toLocalString()方法
  * join():返回以不同分隔符构建的字符串
  * push(),pop(),shift(),unshift():分别为将参数逐个添加到数组末尾并返回数组长度，从数组末尾移除最后一项然后返回移除的项，移除数组的第一个项并返回该项，在数组前端添加任意个项并返回数组长度
  * reserve(),sort():反转数组的顺序；升序排列数组，可接受一个比较函数作为参数进行排序
  * contact():基于当前数组所有项创建一个新数组，将两个数组进行连接，若传入的不是数组则添加到结果数组的末尾
  * splice():不会影响原数组，参数分别为起始位置和结束位置。删除(要删除的第一项位置，要删除的项数)；替换(起始位置，0，要插入的项) ；删除(起始位置，要删除的项数，要插入的项)
  * IndexOf(),lastIndexOf():参数为要查找的项和查找起点位置的索引(可选)。没有找到返回-1
  * 迭代方法
    * every():对数组中的每一项运行给定函数，如果该函数对每一项都返回true则返回true
    * filter():对数组中的每一项运行给定函数，该函数返回true的项形成的数组
    * forEach():对数组的每一项运行给定函数，该函数没有返回值
    * map():对数组的每一项运行给定函数，返回每次函数调用的结果形成的数组
    * some():对数组的每一项运行给定函数,如果该函数对任一项返回true则返回true
  * reduce(),reduceRight():参数(前一个值，当前值，项的索引，数组对象)，函数返回的任何值会作为第一个参数传给下一项

## Date类型

使用new操作符创建一个Date对象

* Date.parse()：接收一个表示日期得到字符串参数，然后根据这个字符串返相应的日期毫秒数
* Date.UTC()：也是返回日期的毫秒数，参数分别是年份，基于0的月份，月中的哪一天，0-23的小时数分钟以及毫秒数
* Date.now()：调用这个方法的日期和事件的毫秒数
* toLocalString()：按照与浏览器设置的地区响应的格式返回日期和时间
* toString()：返回带有时区信息的日期和时间

## RegExp类型

* 匹配模式:g表示全局，将被应用于所有字符串，而非在第一个匹配时终止；i表示不区分大小写；m表示多行
* 元字符必须经过转义`([{\^$|?*+.}])`
* 实例属性:global是否设置了g标志；ignoreCase是否设置了i标志；multiline是否设置了m标志；以上都返回布尔值；source返回正则表达式的字符串表示；lastIndex开始搜索下一个匹配项的字符位置
* 实例方法:exec()接收要应用模式的字符串作为参数，返回包含第一个匹配项信息的数组，不设置为全局时只匹配第一个；test()接收字符串参数，匹配则返回true。配合捕获组使用RegExp.$1.......

## Function类型

* 不推荐使用函数表达式进行声明，需要解析两次代码，降低性能。解析器会率先读取函数声明，并在其执行任何代码之前可访问，函数表达式只解析器执行到所在的代码行才会被解释执行

* 函数可以作为值传递给另一个函数，但是要访问函数的指针而不执行函数，需要去掉括号
* arguments主要用途是保存函数的参数，callee属性指向拥有这个arguments对象的参数，caller保存着调用当前函数的引用

```javascript
function factorial(num){
    if(num <= 1){
        return 1;
    }else{
        return num * factorial(num - 1)
    }
}
//相比之下降低了耦合性
function factorial(num){
    if(num <= 1){
        return 1;
    }else{
        return num * arguments.callee(num - 1)
    }
}
```
## 基本包装类型

* 与引用类型的区别：主要在于对象的生存周期，使用new操作符创建的引用类型的实例，在执行流离开作用域之前都一直保存在内存中。自动创建的基本包装类型，只存在于一行代码执行的瞬间然后立即销毁，所以不能在运行时为基本包装类型添加属性和方法
* 每读取一个基本包装类型值，后台就会创建一个对应的基本包装类型的对象

## Number类型

* valueOf()返回对象表示的基本类型的数值。
* toString(),toLocalString()：返回字符串形式的数值，可传递一个数字作为参数，返回该进制下的字符串
* toFixed()：按照指定的小数返回沪指的字符串表示，会四舍五入
* toExponential()：返回以指数表示法表示该数值的字符串形式，可传入一个参数指定小数位数
* toPrecision()：按指定的参数返回固定位数的数值字符串格式，可为指数形式

## String类型

* 每一个实例属性都有length方法
* 字符方法
  * charAt(),charCodeAt()：以单字符串的形式返回给定位置的那个字符串，charCodeAt()返回的是编码
  * 可以通过方括号中指定下标访问字符串中的字符
* 字符串操作方法
  * contact()：将一个或多个字符串拼接起来，返回拼接得到的新字符串。接受任意多个参数进行拼接。使用+j进行拼接更为简便易行
  * slice(),substr,substring()：都会返回被操作字符串的一个子字符串，都接受一个或两个参数。第一个参数指定子字符串开始的位置，第二个参数表示子字符串到哪里结束。如果没有传递第二个参数，则以字符串长度作为结束位置。不会修改字符串本身的值
    * slice()和substring()第二个参数指定的是字符串的最后一个字符后面的位置，substr()第二个参数指定的是返回的字符串个数。
* 字符串位置方法
  * IndexOf()和lastIndexOf()：搜索给定的子字符串然后返回子字符串的位置没有找到则返回-1，可以接受第二个参数，表示从哪个位置开始搜索。在指定第二个参数情况下，可以循环调用来找到所有匹配的字符串。
* trim()：清除前置和后缀的空格
* toLowerCase(),toUppercase(),toLocalLowerCase(),toLocalUpperCase()：大小写转换，后两者针对特殊地区
* 模式匹配方法：
  * match()：接收一个参数，正则或RegExp对象与exec()方法相同
  * search()：参数与match()相同要求，返回字符串中第一个匹配的索引
  * replace()：接收两个参数，正则或RegExp与一个字符串或函数，替换所有需指定全局匹配
* split()：基于指定分隔符将字符串分割成多个子字符串，并将结果放在一个数组中，可接受第二个参数指定数组的大小
* localCompare()：比较两个字符串。字符串排在参数字符串之前返回-1；相同返回0；之后返回1.
* fromCharCode()：接收一或多个字符编码，将他们转换为字符串

## 对象Object类型

* 对象的数据属性：包含一个数据值的位置。在这个位置可以读取和写入值。
  * Configurable：表示能否通过delete删除属性从而重新定义新属性，能否修改属性的特性，或者能否把属性修改为访问器属性。
  * Enumerable：表示能否for-in循环返回属性。
  * Writable：表示能否修改属性的值。
  * Value：包含这个属性的数据值

* Object.defineProperty()
  * 修改属性默认的特性，该方法接收三个参数，分别是属性所在的对象，属性的名字和一个描述符对象。描述符对象的属性必须是configurable,enumerable,writable和value。设置其中的一个或多个值，可以修改对应的特性值
  * 把configurable属性设为false，表示不能从对象中删除属性。如果对这个属性调用delete，在严格模式下回导致错误。一旦把属性定义为不可配置的，就不能把它再变回可配置了。此时再调用该方法修改writable之外的特性都会导致错误

```javascript
var person = {};
Object.defineProperty(person,"name",{
	writable:false,
	value:"Nicholas"
})
alter(person.name)  //Nicholas
person.name = "Grey"
alter(person.name)  //Nicholas
```

* 对象的访问器属性：不包含数据值，包含一个getter和setter函数(不是必须的)，在读取访问属性时，会调用getter函数，这个函数负责返回有效的值。在写入属性时调用setter函数并传入新值，这个函数负责决定如何处理数据。以下是他的特性
  * Configurable：表示能否通过delete删除属性从而重新定义新属性，能否修改属性的特性，或者能否把属性修改为访问器属性。
  * 表示能否for-in循环返回属性。
  * Get：在读取属性时调用，默认值为undefined
  * Set：在写入属性时调用，默认值为undefined
* 访问器属性不能直接定义，必须使用Object.defineProperty()的方法来定义。

```javascript
var book = {
	_year:2004,
	edition:1
}
Object.defineProperty(book,"year",{
	get:function(){
		return this._year;
	},
	set:function(newValue){
		if(newValue > 2004){
			this._year = newValue;
			this.edition += newValue -2004
		}
	}
})
book.year = 2005;
alert(book.edition)    //2
//_year前面的下划线是一种常用的记号，用于表示只通过对象方法访问的属性
```

* 定义多个属性：Object.defineProperties()
  * 利用这个方法可以通过描述符一次定义多个属性。接收两个参数分别是：添加和修改其属性的对象，第二个对象的属性与第一个对象中要添加或修改的属性一一对应

```javascript
var book = {};
Object.defineProperties(book,{
	_year:{
		value:2004
	},
	edition:{
		value:1
	},
	year:{
		get:function(){
		return this._year;
		},
		set:function(newValue){
			if(newValue > 2004){
				this._year = newValue;
				this.edition += newValue -2004
			}
		}
	}
})
```

* 读取属性的特性：Object.getOwnPropertyDescriptor()，可以取得给定属性的描述符
  * 接收两个参数：属性所在的对象和要读取其描述符的属性名称。返回值是一个对象

```js
//以上述对象为例
var descriptor = Object.getOwnPropertyDescriptor(book,"_year");
alert(descriptor.value)  //2004
alert(descriptor.configureable)  //false
alert(typeof descriptor.get)  //undefined

var descriptor = Object.getOwnPropertyDescriptor(book,"_year")
alert(descriptor.value)  //undefined
alert(descriptor.enumerable)  //false
alert(typeof descriptor.get)  //"function"
```

* 关于对象的复制

### 强制类型转换

将值从一种类型转换为另一种类型通常称为类型转换，这是显式的情况；隐式的情况称为强制类型转换

```js
var a = 42;
var b = a + ""  //隐式类型转换
var c = String(a)  //显式强制类型转换
```

toString()方法转换后的单元字符串会用  ,  连接起来

JSON.stringify()在对象中遇到undefined,function和symbol等对象都不符合JSON的解构标准，会自动忽略，在数组中则返回null(可选参数space，用来指定每一级缩进的字符数)

ToNumber：true 转换为 1， false 转换为 0。 undefined 转换为 NaN， null 转换为 0  



---



## 数据类型：值类型和引用类型

* 基本类型是简单的数据段，引用类型指那些可能由多个值构成的对象。复制引用类型值时会将存储在变量对象中的值复制一份放到为新对象分配的空间中，不同的是这个值的副本实际上是一个指针，引用的是堆中的同一个对象，因此改变其中的一个变量就会影响另一个值的相同变量
* 检测值类型typeof，检测引用类型的值instanceof

**基本类型(值类型)：**String，Number，boolean，undefined，null，Symbol

**引用类型(对象类型)：**Object，Date，Function，Array。后三者都是特殊的对象、

**新增的：**基本数据类型：bigint

#### 内存的分类

**栈：**全局变量和局部变量

**堆：**存放对象，一般负责Object这类引用类型的储存，由垃圾回收机制释放或手动释放

当脚本调用一个函数时，js解析器把函数推入函数调用栈并执行，运行结束后将他从栈中推出

#### 基本类型

* 基本类型的值不能添加属性和方法
* 基本类型的值是存放在栈中的，也就是栈内存
* 基本类型能够使用一些包装类使用的方法是因为这样使用时js会将其转为一个对象，这样他就可以使用对象的特性比如他原型链中的方法，用完后就会抛弃对象的性质重新转变为基本的数据类型

#### 引用类型

* 引用类型可以添加删除属性和方法
* 引用类型同时保存在栈内存和对内部才能，JavaScript不能直接访问内存中的位置，也就是说不能操作对象的内存空间，所以他访问一个引用类型的值是按引用访问的。栈用来存放保存的变量的标识符和指向堆内存中这个对象的指针。也就是这个对象在堆内存的地址；引用类型的赋值也就是为栈内存中的指针赋值

#### 关于封装对象：基本类型为什么能够调用方法

基本类型值没有.length和.toString这样的属性和方法，需要通过封装对象访问。如果需要经常使用到这些属性和方法，从一开始就创建一个封装对象更为方便。但这样会降低代码性能，所以应使用基本类型值而不是new String()之类的。这样JavaScript引擎会自己决定什么时候用封装对象

如果想得到封装对象中的基本类型值，可以使用valueOf()函数

### 深浅拷贝

**数组的浅拷贝：**比如数组，可以利用slice，contact方法返回一个新数组的特性来实现拷贝，但假如数组中嵌套了对象或者数组的话，使用contact方法克隆并不完整，只会拷贝对象和数组的引用，这样无论在新旧数组中进行修改，两者都会发生变化，这种就称为数组的浅拷贝

**深拷贝数组的方法：**

```js
var arr = ['old', 1, true, ['old1', 'old2'], {old: 1}]
var new_arr = JSON.parse(JSON.stringify(arr));
console.log(new_arr)
```

原理是通过json对象中的stringify可以把一个js对象序列化为一个JSON字符串，parse可以把json字符串反序列化为一个js对象，通过这两个方法也可以实现对象的深复制。但这个方法不能拷贝函数

**实现对象或数组的浅拷贝**

```js
var shallowCopy = function(obj){
	if(typeof obj !== 'object'){
		return
	}
	var newObj = obj instanceof Array ? [] : {};
	for(var key in obj){
		if(obj.hasOwnProperty(key)){
			newObj[key] = obj[key]
		}
	}
	return newObj;
}
```

**实现数组或对象的深拷贝**

```js
var deepCopy = function(obj){
	if(typeof obj !== 'obj'){ return }
	var newObj = obj instanceof Array ? [] : {};
	for(var key in obj){
		if(obj.hasOwnProperty(key)){
			newObj[key] = typeof obj[key] === 'object' ? deepCopy(obj[key]) : obj[key]
		}
	}
	return newObj
}
```





---



## 关于类型判断类型与相等判断

#### typeof：

类型判断时使用小写。可以判断undefined/数值/字符串/布尔值/function。不能判断null/object/array

* 判断基本类型会直接返回该数据类型的字符串表达
* 判断引用类型时除了function都会显示object
* 判断没有定义的变量会显示undefined
* 对null使用时会返回一个Object，原理是不同的数据类型在底层是以二进制形式存储，如果前三位为0，那么判断为对象，null的前三位为0

#### instanceof：

判断一个对象是否是一个类的实例，或者是否是一个对象的原型链下层

#### ===：

可以判断undefined和null



---



## 严格模式

**设立严格模式的目的：**

* 清除JavaScript语法的不合理，不严谨，不安全的地方，保证代码安全运行减少一些怪异行为
* 提高编译器效率，增加运行速度

**有两种调用方法，分别针对整个脚本文件与单个函数：**"use strict"；针对整个脚本文件的方法不利于文件，更好的做法是借用第二种方法将整个脚本文件放在一个立即执行的匿名函数中

**对语法与行为的改变：**

* 变量都必须先使用var声明再使用
* 只允许静态绑定：属性和方法归属于哪个对象，在编译阶段就确定这样有利于编译效率的提高
  * 禁止使用with语句，因为with无法在编译时就确定属性到底归属哪个对象
  * 创设了eval作用域：正常模式下eval语句的作用域取决于它处于全局作用域还是处于函数作用域，严格模式下eval语句本身就是一个作用域不能够再生成全局变量了，它所生成的变量只能用于eval内部
* 增强的安全措施：
  * 禁止this关键字指向全局对象，使用构造函数时如果忘了加new，this不再指向全局对象而是报错
  * 禁止在函数内部遍历调用栈
  * 禁止删除变量：只有configurable设置为true的对象属性才能被删除
  * 显示报错：比如对一个对象的只读属性进行赋值，正常模式下只会失败而不会报错，严格模式下会报错
  * 重名错误：
    * 对象不能有重名的属性：正常模式下后面的属性会覆盖前面属性的值
    * 函数不能有重名的参数：正常模式下，如果函数有多个重名的参数可以使用arguments[i]读取
  * 禁止八进制表示法：整数第一位如果是0将报错
  * arguments对象限制
    * 不允许对arguments赋值
    * arguments不再追踪参数的变化
    * 禁止使用arguments.callee
  * 函数声明必须在顶层
  * 新增了一些保留字比如let,public ,static,yield,oacjage,private,interface
比如在严格模式下this的默认绑定就会绑定到undefined上，不是严格模式就会绑定到全局对象上



---



### 关于几个函数

* JavaScript没有重载，如果定义了两个名字相同的函数，后面的会覆盖前面的

* 匿名函数
  * 比如说setTimeout中调用的方法，他的function没有名称标识符。函数表达式可以匿名但函数声明不可以省略函数名，
  * 匿名函数的缺点
    * 在追踪调试时不会显示出具体函数名
    * 没有函数名，函数调用自身时只能通过arguments.callee引用
    * 降低了代码的可读性
* 立即执行函数
  * 将函数包含在一对括号中，通过在末尾添加()可以立即执行函数
  * 可以形成匿名函数表达式，也可以将他作为一个参数传递
  * 可以倒置代码的执行顺序，将要运行的函数放在第二位，在立即执行函数执行之后当做参数传入













































### 关于变量提升

var a = 2。JavaScript会将其看成两个声明，分别是var a和a=2.第一个声明是在编译阶段进行的。第二个声明会等待执行阶段。也就是说只有声明本身会被提升，赋值操作会留在原地。函数声明也会被提升，但函数表达式不会被提升。

* 函数会首先被提升，然后才是变量。所以要注意覆盖问题。
* 一个普通块内部的函数声明通常会被提升到所在的作用域顶部

#### 间歇调用和超时调用

* 用来调度代码在特定的时刻执行，间歇调用为每隔指定时间就执行一次代码，超时调用为指定时间过后执行代码。
* 第一个参数可为JavaScript字符串或一个函数，但传递字符串可能会造成性能损失。
* 可通过clearTimeout()与clearInterval()取消超时和间接调用

#### BOM中的常用对象

window对象是BOM的核心对象，可听过他调整窗口位置大小以及打开新窗口。，location对象用来改变浏览位置，也就是当前的页面；navigator对象识别客户端浏览器，screen屏幕，history历史

#### for,for...in,for...of区别

* for...in:可以用来枚举对象的属性，for(let key in object){} 此处let操作符不是必需的，这是为了保证使用局部变量

#### break和continue区别
* break语句会立即退出循环，强制继续执行循环后面的语句
* continue退出循环后会从循环的顶部继续执行，也就是跳过当次循环

#### 对象属性的访问

* 一般使用点表示法和方括号表示法，使用方括号表示法时应将要访问的属性以字符串的形式放在方括号中
* 方括号表示法的主要优点是可以通过变量来访问属性，但一般建议使用点表示法

### 内置类型

null；undefined；boolean；number；string；object；symbol；除对象object之外，其他统称为基本类型

可以用typeof运算符来查看值的类型，它返回的是类型的字符串值

```js
typeof null === 'object'
typeof function a(){} === 'function'
```

js的变量没有类型，只有值才有。也就是说变量可以随时持有任何类型的值

### 数值比较

```js
-0 === 0;
//可以通过Object.is()判断两个值是否绝对相等
console.log(Object.is(-0,0));  //false
console.log(NaN === NaN);  //false
console.log(Object.is(NaN,NaN));  //true
```

### call(),apply(),bind()

* call,apply：在特定的作用域内调用函数，实际上等于设置函数体内this的对象
  * apply()接收两个参数(在其中运行函数的作用域，参数数组)第二个参数可以使Array的实例也可以使arguments对象
  * call()接收两个参数(this值，逐个列举其余参数)，与apply()区别于两者区别接收参数的方式不同
  * 功能：能够扩展函数运行的作用域，用这两个方法扩展作用域的好处是对象不需要与方法有任何耦合关系
* bind：会创建一个实例，其this值会被绑定到传给bind函数的值。比如传入一个对象o，则this值指向o。他会返回一个新的函数，这个函数不会马上执行

#### 相等，全等，Object.is

* ==存在强制转换number,null==undefined
* Object.is()：+0  != -0 ,NaN ==NaN

### 数组去重

一：indexOf循环去重

二：ES6 Set去重；Array.from(new Set(array))

三：Object 键值对去重；把数组的值存成 Object 的 key 值，比如 Object[value1] = true，在判断另一个值的时候，如果 Object[value2]存在的话，就说明该值是重复的。

### 箭头函数的this

* 箭头函数没有this，this绑定的是最近一层非箭头函数的this
* 不能通过new操作符调用
* 获取arguments对象[...rest]

#### 间歇调用和超时调用

* 用来调度代码在特定的时刻执行，间歇调用为每隔指定时间就执行一次代码，超时调用为指定时间过后执行代码。
* 第一个参数可为JavaScript字符串或一个函数，但传递字符串可能会造成性能损失。
* 可通过clearTimeout()与clearInterval()取消超时和间接调用

#### BOM中的常用对象

window对象是BOM的核心对象，可听过他调整窗口位置大小以及打开新窗口。，location对象用来改变浏览位置，也就是当前的页面；navigator对象识别客户端浏览器，screen屏幕，history历史

#### json

* json其中数据类型可为简单值，对象和数组；要求给属性加引号

### 获得对象上的属性

* for(let i in obj)一次访问一个对象及其原型链中的可枚举属性名称
* object.keys:返回一个数组，包括所有可枚举的属性名称
* object.getOwnPropertyNames:返回一个数组包含不可枚举的属性

### Script标签的使用

* async：设置异步脚本，表示立即下载脚本但不阻碍解析脚本之后的文档，而且一旦下载完就立即异步执行，目的是不让页面等待下载执行这个脚本从而先加载其他内容。async脚本之间不按照顺序执行而是谁先下载完谁执行
* defer：设置延迟，立即下载脚本但延迟到文档完全解析和显示之后按照顺序执行
* src：地址
* type："text/javascript"

### 代码间变量方法共享的条件

代码块可以使用之前出现过也就是预处理的变量和方法，但无法共享之后出现的变量和方法

### 关于js的单线程

同一时间只能做一件事。JavaScript作为浏览器脚本语言主要用途是和用户互动以及操作DOM，如果他有两个线程，一个在DOM上添加内推一个删除了这个节点，这就会引起复杂的同步问题。但为了利用多核cpu，html5提出了允许JavaScript创建多个线程，但是子线程完全受主线程控制且不得操作DOM

### js的执行过程

语法检测。词法分析(预编译)：创建去哪聚对象，将var声明的变量进行提升放入全局中不复制，将函数提升。执行

### commonjs和ES6 Module的区别

* 模块导入导出的语法不同
  * commonjs是module.exports，使用exports导出，require导入
  * ES6是export导出，import导入
* commonjs是运行时加载模块；ES6在静态编译期间就确定模块的依赖
* ES6在编译期间会将所有import提升到顶部；commonjs不会提升require
* commonjs导出的是一个值拷贝，会对加载结果进行缓存，一旦内部再修改这个值，则不会同步到外部；ES6是导出一个引用，内部修改可以同步到外部
* 原理不同。
  * commonjs是当模块遇到循环加载时，返回的是当前已经执行的部分的值，而不是代码全部执行后的值
  * ES6是动态引用，如果使用import从一个模块加载变量，那些变量不会被缓存，而是成为一个指向被加载模块的引用
* commonjs顶层的this指向模块本身，ES6顶层的this指向undefined
* commonjs中的一些顶层变量在ES6中不存在，比如module，exports，arguments，__filename






















# 重点内容



## 垃圾收集机制的原理

* 原理：找出不再继续使用的变量，然后释放其占用的内存  
* 清除策略: 
  `引用计数:`跟踪记录每个变量被引用的次数，当生声明一个变量并将一个引用类型值赋给该变量时，这个值的引用次数就是1，如果同一个值又被赋给另一个变量，则该值的引用次数+1。如果这个值医用的变量又取得了另一个值，那么这个值的引用次数减一。当垃圾收集器运行时会释放引用次数为0的值所占用的内存。(将值赋为null可消除循环引用问题) 
  `标记清除:`当变量进入环境(声明变量)时，会将变量标记为进入环境。当白那两离开环境时，会将其标记为离开环境。垃圾收集器会去掉环境中的变量以及环境中的变量引用的标记变量，再此之后再被加上标记的变量将被视为准备删除的变量，因为你环境中的变量已经无法访问到这些变量了。



---



## 作用域

* 作用域是一套规则，用于确定在何处以及如何查找标识符  
* 用来管理引擎如何在当前作用域以及嵌套的子作用域中根据标识符的名称进行变量查找  
* 它分为词法作用域与块级作用域，词法作用域是由写代码时将变量和块级作用域写在那里决定的
* 词法作用域的查找流程，先从最内部的作用域开始查找，引擎无法找到需要的变量就会去上一层嵌套的作用域中查找，作用域查找会在找到第一个匹配的标识符时停止，在多层的作用域中可以定义同名的标识符，内部的标识符即遮蔽了外部的标识符。  换种说法就是，当代码在环境中执行时，会创建变量对象的一个作用域链，保证对有权访问的所有变量和函数进行有序访问。内部环境可以通过作用域链访问所有的外部环境，外部环境不能访问内部环境的任何变量与函数。  
  全局变量会自动成为全局对象，所以可以通过全局对象属性的引用来进行访问，这样可以访问被同名变量遮蔽的全局变量。
* 此处顺带讲解with语句，它和eval都可以改变词法作用域，但是会降低性能。 
  with作用是将代码的作用域设置到一个特定的对象中，语法:with (expression) statement
  例 `with(location){var url = href}`，在他的代码块内部，每个变量先被认为是一个局部变量，而如果在局部环境中找不到该变量的定义，就会查询location对象中是否有同名属性。若有，则以location对象属性的值作为变量的值 

#### 关于作用域
关于作用域首先要说变量的赋值，变量的赋值会执行两个动作，首先会在当前作用域内声明一个变量，然后在运行时引擎就会在作用域内查找该变量，如果找到就会对他赋值。总的来说作用域是一套规则，用于确定在何处以及如何查找标识符。

* 关于作用域的嵌套，当一个块或一个函数嵌套在另一个块或者另一个函数中时，就会发生作用域的嵌套。这样的话如果在当前作用域中没办法找到某个变量时，引擎就会在他外层的作用域内查找，直到找到这个变量，或者是到全局作用域为止
* 词法作用域
  * 作用域的查找流程，先从最内部的作用域开始查找，引擎无法找到需要的变量就会去上一层嵌套的作用域中查找，作用域查找会在找到第一个匹配的标识符时停止，在多层的作用域中可以定义同名的标识符，内部的标识符即遮蔽了外部的标识符。  换种说法就是，当代码在环境中执行时，会创建变量对象的一个作用域链，保证对有权访问的所有变量和函数进行有序访问。内部环境可以通过作用域链访问所有的外部环境，外部环境不能访问内部环境的任何变量与函数。
  * 全局变量会自动成为全局对象，所以可以通过全局对象属性的引用来进行访问，这样可以访问被同名变量遮蔽的全局变量。

* 函数作用域
  * 每声明一个函数都会为其创建一个函数的作用域，属于这个函数的所有变量都可以在整个函数的范围内使用和复用
  * 这段代码中的任何声明的变量或函数都被绑定在这个作用域内而不是之前的作用域，通过函数作用域也可以将一些变量进行隐藏，让外部的作用域无法进行访问。
  * 问题：需要声明一个具名函数，函数的名称就污染了全局作用域，然后必须通过显示调用才能运行其中的代码
    * 解决：(function foo(){...})();这也就是立即执行函数，意味着foo只能在他自己所代表的位置被访问，外部作用域则不行，其他的函数名被隐藏在自身中不会污染全局变量
  * 函数声明和函数表达式之间最重要的区别也就是把他们的名称标识符会被绑定在声明地方
* 块作用域
  * ES5中只有全局作用域和函数作用域，可能会导致内层变量覆盖外层变量，用来计数的循环变量泄露为全局变量
  * ES6新增了块级作用域，比如let,const等定义的块级作用域



---



## 闭包

JavaScript语言的函数内部可以直接读取全局变量，但函数外部无法读取函数内部的局部变量。(函数内部声明变量的时候一定要使用var命令不然会声明为全局变量)。

但有时需要用到函数内部的变量，就需要使用闭包，在函数的内部再定义一个函数。

```js
function out(){
    var n = 99;
    function in(){
        alter(n);
    }
}
//闭包写法
function out(){
    var n = 99;
    function in(){
        alter(n);
    }
    return in;
}
```

函数in在函数out的内部，这是out的所有局部变量对in都是可见的，但反过来就不行了。既然in可以读取out中的局部变量，那么只要把in作为返回值，就可以在out外读取它的内部变量了。

闭包就是能够读取其他变量内部变量的函数。

闭包的作用：可以读取函数内部的变量；让这些变量的值始终保存在内存中

```js
function f1(){
    var n=999;
    nAdd=function(){n+=1}  //没有加var是一个全部变量，也是一个匿名函数
    function f2(){
        alert(n);
    }
    return f2;
}
var result=f1();
result(); // 999
nAdd();
result(); // 1000
```

result就是闭包f2函数，运行两次的值改变了说明函数f1的局部变量值一直保存在内存中，并没有被垃圾回收机制清除**（引出垃圾回收机制）**。没有被清除的原因是f1是f2的父函数，而f2被赋给了一个全局变量result，导致f2始终在内存中，而f2依赖于f1，所有f1的局部变量也一直保存在内存中

注意点：内存消耗大会造成性能问题，解决方法是在退出函数前将不使用的局部变量删除；闭包会在父函数外部改变父函数内部的值。

---

闭包的创建：一个函数内嵌套另一个函数，并且将这个函数return出去，然后将这个return出来的函数保存到一个变量中，这就创建了一个闭包

能够读取其他函数内部变量的函数，或者子函数在外面调用，子函数所在的父函数作用域不会被释放。也就是在外部函数执行后，一般他的整个内部作用域都会被垃圾回收机制销毁释放不再使用的内存空间，而闭包可以使它不被销毁，因为他本身仍旧在使用

指有权访问另一个函数作用域中的变量的函数。闭包就是函数的局部变量集合，只是这些局部变量在函数返回后会继续存在。就是函数的堆栈在函数返回后并不释放，可以理解为这些函数堆栈不在栈上分配而是在堆上分配。当在一个函数内定义另一个函数就会产生闭包

* 闭包满足两个条件：即使上下文销毁依然存在；在代码中引入了自由变量
* 也就是说当函数可以记住并访问所在的词法作用域，即使函数是在当前词法作用域之外执行，就产生了闭包。
* 应用，比如for循环用定时器输出i，延迟函数的回调会在循环结束才执行。使用闭包可以让他访问外部变量且正确执行；还可以实现模块模式，为创建内部作用域而调用一个包装函数包装函数的返回值至少包括一个对外部函数的引用，这样就会创建涵盖整个包装函数内部的作用域的闭包
* 匿名自执行函数：变量如果不加上var关键字就默认会添加到全局对象的属性上去。这样临时变量加入全局会有很多坏处，比如别的函数可能误用这些变量造成全局对象过于庞大，影响访问速度(因为变量的取值是需要从原型链上遍历的)。除了每次都要使用的变量外，有些函数只需要执行一次，其内部变量无需维护，可以使用闭包
* 结果缓存：若有一个函数处理调用起来很耗时间，就需要将计算出来的值储存起来，当调用这个函数时先在缓存中查找，如果找不到则进行计算更新缓存，如果找到了就直接返回查找到的值。闭包可以做到这点因为它不会释放外部的引用从而使函数内部的值得以保留

---

* 能够读取其他函数内部变量的函数，或者子函数在外面调用，子函数所在的父函数作用域不会被释放
* 就是函数的局部变量集合，只是这些局部变量在函数返回后会继续存在。闭包就是函数的“堆栈”，在函数返回后并不会释放。也可以理解为，这些函数堆栈不再栈上分配而是在堆上分配(此处引出堆栈的区别)。当一个函数定义在另一个函数内就会引出闭包
* 闭包满足两个条件：即使上下文销毁依然存在；在代码中引入了自由变量
* 使用闭包的原因以及应用：
  * 匿名自执行函数：变量如果不加上var关键字就会默认地添加到全局对象的属性上去，这样别的函数可能误使用这些变量；变量的取值需要从原型链上遍历，影响访问速度，造成全局对象过于庞大；所以有点函数只需要执行一次，内部变量无需维护，这时可以使用闭包(整理思路，闭包和立即执行函数的区别)
  * 闭包可以做到结果缓存，比如一个函数对象处理过程非常耗时，可以将他的结果进行缓存，因为闭包不会释放外部的引用，所以函数内部的值可以保留下来。(案例)
  * 模仿块级作用域
  * 单例模式(知识补充)



---



## this

this可以隐式传递一个对象的引用，引用的是函数据以执行的环境对象。

this是在运行时绑定的，并不是在编写时绑定，它的上下文取决于函数调用时的各种条件。this的绑定和函数声明的位置没有任何关系，只取决于函数的调用方式。当一个函数被调用时，会创建一个活动记录(也就是执行上下文)。这个记录包含函数在哪里被调用，函数调用的方法，传入的参数信息等。this就是记录的其中一个属性，会在函数执行的过程中调用

* 调用位置：是函数在代码中被调用的位置(而不是声明的位置)

```js
//关于调用栈和调用位置
function baz(){
	//当前调用栈是baz,因此当前调用的位置是全局位置
	console.log("baz");
	bar()  //bar的调用位置
}
function bar(){
	//当前的调用栈是baz-bar,因此当前的调用位置是在baz中
	console.log("bar");
	foo()  //foo的调用位置
}
function foo(){
	//当前的调用栈baz-bar-foo,当前调用位置在bar中
	console.log(foo);
}
baz();  //baz调用的位置
```

* this的绑定规则：
  * 默认绑定：独立函数调用，可以把这条规则看作是无法应用其他规则时的默认规则。默认绑定this指向全局对象。
  * 隐式绑定：考虑调用位置是否有上下文对象，或者说是否被某个对象拥有或者包含
  * 显示绑定：不在对象内部包含引用，而是在某个对象上强制调用函数.可以通过函数的call和apply方法
  * new绑定：函数或方法调用之前带有new关键字，构成构造函数的调用。
    * 没有return，计算结果是这个新对象的值
    * 有return没有指定返回值，忽略返回值，使用该新对象作为调用结果
    * 有返回值，调用表达式的值就是这个对象

```js
//默认绑定
function foo(){
	console.log(this.a);
}
var a = 2;
foo();  //2
//隐式绑定
function foo(){
	console.log(this.a);
}
var obj = {
	a:2;
	foo:foo
};
obj.foo()
//显式绑定
function foo(){
	console.log(this.a);
}
var obj = {
	a:2
}
var bar = function(){
	foo.call(obj)
}
bar()  //2
//new绑定
function foo(a){
	this.a = a;
}
var bar = new foo(2);
console.log(bar.a);
```

默认绑定时不能使用严格模式，如果使用严格模式那么全局对象将无法进行默认绑定，this会绑定到undefined

隐式绑定中的隐式丢失：也就是隐式绑定的函数会丢失绑定对象，应用默认绑定，从而把this绑定到全局对象或者undefined上

显式绑定中第三方库的许多函数以及js的许多内置函数，都提供了一个可选参数确保函数使用指定的this

* 优先级问题：按照下面的顺序进行判断
  * 函数是否在new中调用，如果是的话this绑定的是新创建的对象
  * 函数是否通过call，apply显示绑定或硬绑定调用。如果是的话this指向的就是绑定的对象
  * 函数是否在某个上下文对象中调用(隐式绑定)。如果是的话this绑定的就是上下文对象
  * 如果都不是的话使用默认绑定，严格模式下绑定undefined，否则绑定到全局对象
* this中的绑定例外



---



## Prototype

是对于其他对象的引用，几乎所有对象在创建时prototype属性都会被赋予一个非空的值。

##### 作用1

关于他的用处：当试图引用对象的属性时会触发get操作，对于get操作来说，第一步就是检查对象本身是否拥有这个属性，有的话就使用它。但是如果这个属性不再该的对象中，就需要使用对象的prototype链。比如无法获取这个对象中的a属性，就会继续访问该对象的prototype链。这个查找的过程会持续到匹配到属性名或查找完整条prototype链。使用for...in遍历对象或in操作符检查属性在对象中是否存在时，都会查找对象的整条原型链

* 此处提一下Object.create()方法，会穿件一个对象并把这个对象的prototype关联到指定对象。

* 所有prototype原型链的尽头都会执行内置的Object.prototype

当为对象的属性设置值时，如果对象中包含对应属性则会修改已有的属性值，该属性值会屏蔽其prototype链上的属性值；如果该属性不是存在于该对象中，那么就会去prototype链上遍历，存在以下三种情况：在后两种情况下若想覆盖只能使用Object.defineProperty()

* 如果prototype链上存在该属性并且没有标记为只读，那就会在要设置的对象中添加一个该属性，屏蔽之前属性
* 如果存在且被标记为只读，那么久无法在要设置的对象中设置该属性值，严格模式下还会报错
* 如果存在该属性并且它是一个setter，那就会调用这个setter而不是重新设定

##### 作用2

模仿类：利用了函数的特性：所有函数都会默认拥有一个名为prototype的公有的并且不可枚举的属性，它会指向一个对象，他指向的对象通常被称为原型，通过方法名.prototype的属性引用来访问它。这个对象是在调用new Foo()时创建的，最后会被关联到Foo.prototype指向的那个对象。在js中不能创建一个类的多个实例，只能创建一个对象使他们的prototype关联上同一个对象。new Foo会生成一个新对象，比如a，这个新对象的prototype关联的是Foo的prototype。这个机制通常被称为原型继承。继承意味着赋值操作，但Js默认情况下并不会赋值对象属性，而会在两个对象之间创建一个关联，这样可以通过委托访问另一个对象的属性和函数

```
是实现继承的主要方法，基本思想史利用原型让一个引用类型继承另一个引用类型的属性和方法。
每个构造函数都有一个原型对象，原型对象包含一个指向构造函数的指针。而实例都包含一个指向原型对象的内部指针。
当创建一个函数，就会为该函数创建一个prototype属性，这个属性指向函数的原型对象，默认情况下所有原型对象都会获得一个constructor(构造函数)属性，这个属性是一个指向prototype属性所在函数的指针
prototype的作用是在多个实例对象之间共享数据和方法；通过原型链实现继承
原型链：
每个构造函数都要一个原型对象，原型对象都包含一个指向构造函数的指针，构造函数的实例对象都有一个指向原型对象内部的指针
如果让原型对象等于另一个构造函数的实例对象，此时原型对象内部也包含另一个指向另一个构造函数的原型对象的指针
```

#### 原型继承

````js
function Foo(name){
	this.name = name;
}
Foo.prototype.myName = function(){
	return this.name;
}
function Bar(name,label){
	Foo.call(this,name)
	this.label = label;
}
//创建了一个新的Bar.prototype对象关联到Foo.prototyp
Bar.prototype = Object.create(Foo.prototype);
/*
其他方法
Bar.prototype = Foo.prototype
并不会创建一个关联到Bar.prototype的新对象，只是让Bar.prototype直接饮用Foo.prototype对象
Bar.prototype = new Foo()
会创建一个关联到Bar.prototype的新对象，但他使用Foo的构造函数调用，如果Foo有一些其他的作用比如给this添加属性修改状态之类的就会影响到Bar()的后代
*/

Bar.prototype.myLabel = function(){
	return this.label;
}
varr a = new Bar("a","obj a");
a.myName();//"a"
a.myLabel();//"obj a"
````

修改对象的prototype关联的方法：ES6之前设置\__proto__属性实现，ES6之后可以使用setPrototype方法

#### 检查类的关系

假如有对象a，寻找对象a委托的对象

* 类的角度：instanceof操作符，只能处理对象a和函数之间的关系，不能判断是否通过prototype关联
* 判断prototype反射的方法 Foo.prototype.isPrototypeof(a)。isPrototypeOf可以判断在a的整条prototype链中是否出现过Foo.prototype
* 直接获取一个对象的prototype链 Object.getPrototypeOf(a)

#### 对象关联

prototype就是存在于对象中的一个内部链接，如果在对象上没有找到需要的属性或方法引用，引擎就会继续在prototype关联的对象上进行查找

在ES6之前没有类和继承的概念，js是通过原型来实现继承的。在js中药柜构造函数默认带有一个prototype属性，这个属性值是一个对象，同时这个prototype对象自带有一个constructor属性，这个属性指向这个构造函数，同时每一个实例都会有一个\__proto__属性指向这个prototype对象，可以把这个叫做隐式原型，我们在使用一个实例方法的时候，会先检查这个实例中是否有这个方法，没有的话会检查prototype对象是否有这个方法。



---



## 事件

* HTML中与javascript交互是通过事件驱动来实现的，例如鼠标点击事件onclick，页面的滚动事件onscroll等等
* 事件流是指从页面中接收事件的顺序:事件捕获:从上往下传播，处于目标节点，事件冒泡:从下往上传播，IE只支持事件冒泡。事件的传递定义了元素事件的触发顺序，如果将p元素插入到div元素中，用户点击p元素。事件冒泡先触发的是内部元素，然后冒泡到外部元素；事件捕获是先触发外部元素，然后捕获内部元素
* 事件监听addEventListener：指定事件处理程序的操作，可以简单的控制事件这个方法接收3个参数：
  * 事件的类型(click,mousedown)
  * 事件触发后调用的函数
  * 一个布尔值用于描述是冒泡函数捕获(可选参数)，false为事件冒泡，true为事件捕获
  * 如果DOM节点同时绑定了两个事件监听函数，一个用于捕获一根用于冒泡，绑定在被点击元素上的事件是按照代码添加顺序执行的，其他函数是先捕获再冒泡
  * 移除方法：removeEventListener(事件名，处理函数)
  * IE：attachEvent(事件名，处理函数)；detachEvent(事件名，处理函数)
* 事件模型的常用方法
  * event.stopPropagation:阻止捕获和冒泡阶段中，当前事件的进一步传播
  * event.stopImmediatePropagetion，阻止调用相同事件的其他侦听器
  * event.target：指向触发事件的元素，在事件冒泡过程中这个值不变
  * event.currentTarget = this，时间帮顶的当前元素，只有被点击时目标元素的target才会等于currentTarget
  * 阻止默认行为(例如a标签的跳转，Submit按钮的提交)：event.pretentDefault()；event.returnValue = false；return false；
* 让事件先冒泡后捕获：思路为监听到捕获事件暂缓执行，直到事件冒泡之后再捕获(此处缺一个案例)
* 事件委托：不在事件的发生元素设置监听函数，而是在父元素上设置监听函数。这样做通过事件冒泡，父元素可以监听到子元素上事件的触发，从而做出不同响应。是通过事件冒泡的运行机制实现的。从另一个方面来讲，如果父元素有与子元素相同的事件，那么会从子元素一直冒泡根据嵌套关系向外触发，一直到document/window
  * 例：ul和li标签的监听，不会在li标签上直接添加，而是在ul父元素上添加(缺少代码实例)
  * 好处：适合动态元素的绑定，新添加的子元素也会有监听函数，可以有事件触发机制。减少内存的消耗，提高效率。
* mouseover移入元素会重复触发，有一个冒泡的过程。mouseenter移到元素本身时才会触发事件，不会冒泡



---



## 异步

#### 概念

程序中现在运行的部分和将来运行的部分之间的关系就是异步编程的核心

可以将JavaScript程序写在单个的js文件中，但是这个程序巨虎一定是由多个块构成的，这些块中只有一个是现在执行，其他会在将来执行，最常见的块单位是函数。程序在将来执行的部分不一定在现在运行的部分执行完成之后就立即执行，也就是说现在无法完成的任务将会异步完成，因此并不会出现阻塞行为。

---

标准的ajax请求就不是同步完成的

```js
var data = ajax("http://some.url.1")  //一个封装的ajax函数
console.log(data);
```

这时data中不会包含那个ajax的结果，这意味着ajax函数没有返回任何值可以赋值给变量data。如果ajax能够阻塞到响应返回，那么data的赋值就会正确工作。

但我们不是这样使用ajax的，现在我们发出一个异步请求，在将来才能得到返回的结果。需要得到将来的返回值最简单的方法是使用回调函数

```js
ajax("http://some.url.1",function CallbackFunction(data){
    consloe.log(data)
})
```

附：尽管ajax可以发送同步请求，但它会锁定浏览器的UI按钮菜单滚动条等，并阻塞所有的用户交互

也就是说只要把一段代码包装成一个函数，并制定它在某个事件响应时执行(定时器，鼠标点击，ajax响应等)，就是在代码中创建了一个将来执行的块，也由此在这个程序中引入了异步机制。

**事件循环：**提供了一种机制来处理程序中多个块的执行，且执行每个块时调用JavaScript引擎。

**关于setTimeout()：**并没有把回调函数挂在事件循环队列中，他所做的是一个定时器，但如果事件循环中已经有多个项目，回调就会等待，通常没有抢占的方式直接将其排到队首，这就解释了setTimeOut()定时器的精确到不高，只能保证回调函数不会在指定的时间间隔之前运行。

---

**并行线程：**能够同时发生的事情，就比如说两个代码块中一个的功能是对一个值进行增，另一个对该值乘以2，要是并行就有多重结果

**完整运行：**JavaScript有完整运行的特性，他的代码块一般具有原子性，也就是说他一个代码块中代码会在另一个代码块开始运行之前完成不会被另一个代码块中断，所以程序结果单一。但如果存在多线程，那就可能有不同的结果。

#### 并发进程

比如一个页面，要实现下拉加载更多，就需要同时运行两个"进程"。第一个在用户下拉时响应这些事件发起ajax请求要求新的内容，第二个接收响应把内容展示到页面。同时执行就发生了并发

就是需要发起请求的事件和响应时间同时处理，但JavaScript是单线程一次只能处理一个事件，他们不会同时发生。所以会是事件1或者事件2线发生，通过事件循环机制交替依次运行

**非交互：**如果两个任务彼此不相关相互间没有影响，就可以接受不确定性，他们谁先执行就没有要求

**交互：**两个任务如果需要交流，就需要交互进行协调避免出现竞争。通过异步请求将两个不同页面响应的内容加入到一个数组中，顺序就会受到页面响应时间等的影响不会按既定顺序推入到数组中。可以通过if判断进行协调避免不确定性

**协作：**取到一个长期运行的进程，将其分割成多个步骤或多批任务，使得其他并发进程有机会将自己的运算插入到事件循环队列中交替运行。

#### 任务

#### 语句顺序

#### 回调

回调函数是一个作为变量传递给另外一个函数的函数，它在主体函数执行完之后执行

#### 嵌套回调和链式回调

```js
listen('click',function handle(evt){
    setTimeout(function request(){
        ajax('',function response(){
            ...
        })
    },1000)
})
```

当多个函数嵌套，每个函数代表异步序列的一个步骤，这种代码也就是回调地狱

以上代码为嵌套回调；但是如果将他变为链式回调，也是在代码的执行块中不断跳跃，难以追踪。顺序阻塞式的计划无法很好地映射到回调的异步代码，导致代码逻辑混乱可读性和可修改行都比较困难，这是主要的缺陷。

其次想比与其他代码来说，无法得知回调什么时候调用是否过早或过晚，调用次数太多或太少等问题。

需要解决这种问题就比较复杂，比如要各种条件判断语句，设置超时取消事件，传入一个参数从而保留错误等等。

---

## Promise

通过回调管理异步的缺陷：缺乏顺序性和可信任性。顺序性就是常说的回调地狱，导致代码难以维护。可信任性就是回调过程中无法监控他的状态，得知他是否过早或过晚调用，调用次数多少问题。

```js
function add(getX,getY,cb){
	var x,y;
	getX(function(xVal){
		x = xVal;
		if(y != undefined){
			cb(x+y);
		}
	});
	getY(function(yVal){
		y = yVal;
		if(x != undefined){
			cb(x+y);
		}
	})
}
//fetch为同步或异步函数
add(fetchX,fetchY,function(sum){
	console.log(sum);
})
```

```js
function add(xPromise,yPromise){
    //Promise.all接收一个promise数组并返回一个新的promise，该promise等待数组中所有promise完成
	return Promise.all([xPromise,yPromise])
    //这个promise决议后，取得收到的X和Y值并加在一起
		.then(function(values){
        //value是来自于之前决议的promise的消息数组
			return values[0]+values[1];
		})
}
//fetch函数返回响应值的promise，可能就绪或未就绪
add(fetchX(),fetchY())
//得到一个这两个数组的和的promise，链式调用then来等待返回promise的协议
	.then(function(sum){
		console.log(sum);
	})
```

这段代码中有两层Promise，fetchX和fetchY是直接调用的，他们的返回值(promise)被传给add；这些promise代表的底层值的可用时间可能是现在或将来，但promise保证了行为的一致性，可以按照不依赖与时间的方式追踪值X和Y；第二层是add()函数，通过promise.all()创建并返回promise。通过调用then来等待这个promise。add运算完成后，未来值sum就准备好了可以打印出来，这个等待未来值X和Y的逻辑在add内部

在add内部，promise.all()调用创建了一个promise(等待promiseX和promiseY的决议)，链式调用.then()创建了另外一个promise(这个promise由return value[0]+value[1]这一行立即决议得到加运算的结果)；链add调用终止处调用then，代码借我处实际上操作的是返回的第二个promise；尽管then后面没有链接任何东西，但实际上也创建了一个新的promise

通过promise调用then实际上可以接受两个参数，一个用于完成情况，一个用于拒绝情况，就比如在获取x或y时出错或者在相加的过程中出错，add返回的就是一个被拒绝的promise，传给then的第二个错误处理回调就会从这个promise得到拒绝值

从外部看由于promise封装依赖于等待底层值的完成或拒绝，因此promise可以按照可预测的方式组成而不用担心时序或底层的结果

一旦Promise决议，它就永远保持在这个状态这是它就变成了不变值，可以根据需求多次查看，就是因为promise决议后就是外部不可变的值，可以把这个值传递给第三方并且确信它不会被修改，特别是对于多个地方查看同一个promise的情况。

---

假设要调用一个函数foo执行某个任务，但这个任务可能立即完成也可能需要一段时间才能完成，我们只需要知道foo什么时候结束，就可以进行下一个任务，换句话说就是要通过某种方式在foo完成的时候得到通知

使用回调的话，通知就是任务foo调用的回调，使用Promise的话，就是侦听来自foo的事件，然后在得到通知的时候根据情况继续。

new  Promise(function(){})中传入的函数会立即执行，他有两个参数分别是reject和resolve，这些是Promise的决议函数,resolve通常标识完成，reject标识拒绝

---

识别Promise或者类似Promise就是定义某种称为thenable的东西，将其定义为具有then方法的对象和函数

总的来说Promise就是为了解决回调出现的一些问题：

* 调用过早或过晚或不被调用
  * 调用过早：一个任务有时同步完成，有时异步挖完成，这可能会导致竞态条件。而Promise不必担心这种问题因为即使是立即完成的Promise也无法被同步观察到，也就是说当一个Promise调用then的时候，即使这个promise已经决议，提供给then的回调也总会被异步调用
  * 调用过晚：Promise创建对象调用resolve或reject时，这个Promise的then注册的观察回调就会被自动调度，可以确信这些回调在下一个异步事件点上一定会被触发
* 调用次数过多或过少
* 未能传递所需的环境和参数
* 不显示出可能出现的错误和异常





---



### 宏任务，微任务---JavaScript

js在处异步操作时使用的是事件循环机制：处理顺序：同步任务---异步任务（微任务---宏任务）

微任务操作：Promise；MutationObserver

宏任务：setTimeOut；setInterval；I/O操作

















# 总结

## 作用域和闭包

作用域是一套规则，用于确定在何处以及如何查找变量。比如一个var a = 2;首先var a会在其作用域内声明新变量，在代码执行前进；随后a=2会查找变量a对齐进行赋值。如果要对变量进行赋值就会进行左查询，如果是获取变量的值就会进行右查询

词法作用域意味着作用域是由书写代码时函数声明的位置来决定的。编译的词法分析阶段基本能够知道全部标识符在哪里以及是如何声明的，从而能够预测在执行过程中如何对它查找。进行词法作用域的欺骗eval和with。前者可以对包含一个或多个声明的代码字符串进行演算，并借此来修改已经存在的词法作用域。后者本质上是通过将一个对象的引用当做作用域来处理，将对象的属性当做作用域中的标识符来处理，从而创建了一个新的词法作用域，两个方法都会影响性能

函数作用域，声明在一个函数内部的变量或函数会在所在的作用域中隐藏起来。

块作用域指的是变量和函数不仅可以属于所处的作用域，也可以属于某个代码块内部

所有声明的变量或函数都会被移动到各自作用域的顶端，这个过程被称为提升，声明本身会被提升，而包括函数表达式才内的赋值操作不会被提升

当函数可以记住并访问所在的词法作用域，即使函数是在当前词法作用域之外执行，这时就产生了闭包



## this和对象原型

this实际上是函数被调用时发生的绑定，它指向什么取决于函数在哪里被调用

this绑定对象规则

* 由new调用，绑定到新创建的对象
* 由call和apply调用或者bind，绑定到指定的对象
* 由上下文对象调用，绑定到上下文对象
* 默认：严格模式下绑定到undefined，否则绑定到全局对象

如果要访问的对象中并不存在的一个属性，get操作就会查找对象内部prototype关联的对象，这个关联关系实际上定义了一条原型链，在查找属性时会对它进行遍历。

所有普通对象都有内置的Object.prototype，指向原型链的顶端(比如说原型作用域)。如果在原型链中找不到指定的属性就会停止。比如toString，valueOf之类的一些功能就存在于Object.prototype对象上，因此所有的对象都可以使用他们

关联两个对象最常用的方法是使用new关键词进行函数调用，使用new调用函数时会把新对象的prototype属性关联到其他对象。带new的函数调用通常被称为构造函数调用