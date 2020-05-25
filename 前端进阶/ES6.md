# ES6总结(参考ES6标准入门)

## let和const

### let

用于声明变量，所声明变量只在let命令所在代码块内有效。相比于var，var声明的变量在全局范围内有效。

* 使用let声明的变量不存在变量提升，也就是说如果使用var声明一个变量，在变量声明前就可以使用var声明的那个变量，值为undefined，而let则不会存在变量提升的问题，声明的变量一定要在声明后使用
* 存在暂时性死区，在块级作用域内存在let命令，它声明的变量就绑定这个区域，不再受到外部的影响。比如在外部使用var声明了一个变量，然后在作用域块内使用let再次声明同名变量，在声明前该变量不可用。使用let声明的变量会绑定这个区域。也就是说在使用let声明这个变量之前，该变量在哪里都不可用。
* 不允许重复声明：不能再相同的作用域内重复声明同一个变量，也不能再函数内部重新声明参数。但是可以在不同的作用域内重复声明同一个变量，在对应作用域内能取到对应变量的值。

### 块级作用域

ES5中只有全局作用域和函数作用域，可能会导致内层变量覆盖外层变量，用来计数的循环变量泄露为全局变量

* ES6的块级作用域外层代码块不受内层代码块的影响，允许块级作用域任意嵌套。
* 在块级作用域之中函数语句的行为类似于let，在块级作用域之外不可引用。但是应避免在块级作用域内声明函数
* 使用do可以将块级作用域变为do表达式，即可以返回值

### const命令

声明一个只读的常量，一旦声明常量的值不能改变

* 声明时必须立即初始化
* 只在声明的块级作用域内有效，不会进行变量提升，只能在声明后使用
* 本质：并不是变量的值不可改动，而是指向的那个内存地址不得改动。比如为const创建的对象添加属性，这并不会改变他指向的内训地址值，就可以添加成功
* 如果想将对象冻结，可以使用Object.freeze()方法



##  变量的解构赋值

### 数组的解构赋值

允许按照一定模式从数组和对象中提取值，然后对变量进行赋值

```javascript
let [a,b,c] = [1,2,3];
let [foo,[[bar],baz]] = [1,[[2],3]]
```

* 如果解构赋值不成功，foo的值会等于undefined
* 不完全解构：等号左边的模式只匹配一部分的等号右边的数组，这时解构可以成功。但如果等号右边的不是数组则将会报错
* 只要某种数据解构具有Iterator接口，都 可以使用解构赋值
* 解构赋值允许指定默认值，默认值可以引用解构赋值的其他变量，但该变量需已声明

### 对象的解构赋值

数组的解构赋值是按照次序排序的，变量的解构赋值需要与属性名同名才能取到正确的值。

```javascript
let {foo,bar} = {foo:"aaa",bar:"bbb"}
var {foo:baz} = {foo:'aaa',bar:'bbb'}
```

也就是说对象的解构赋值内部机制是先找到同名属性然后再赋值给对应变量

* 可以用于嵌套结构的对象，可以很方便的将现有对象的方法赋值到某个变量。比如Vue中导入elementui中的组件内容就可以使用这种方法

* ```javascript
  let {log,sin,cos} = Math
  //将Math对象的三个方法赋值到对应的变量上，使用起来就会方便很多
  ```

### 其他

* 字符串也可以解构赋值转换成一个类似数组的对象
* 数值和布尔值的解构赋值
  * 如果解构赋值时等号右边的是数值和布尔值，会先转为对象
* 函数参数可以使用解构赋值，可以为它指定默认值

### 用途

* 交换变量的值    [x,y] = [y,x]
* 将多个值放在对象或数组中通过函数返回，通过解构赋值方便地取出这些值
* 可以将一组参数和变量名一一对应起来
* 提取JSON数据
* 指定函数参数的默认值
* 配合for [key,value] of遍历map结构codePoint

## 字符串的扩展

* 将Unicode值放进{}内可以正确输出超过Unicode范围的字符
* codePointAt()，能够正确处理四个字节储存的字符，返回一个字符的码点
* includes()：返回布尔值，表示是否找到了参数字符串
* startWith()：返回布尔值，表示参数字符串是否在源字符串的头部
* endWith()：返回布尔值，表示参数字符串是否在源字符串的尾部
* includes()，startWith()，endWith()都可以接受第二个参数，表示开始搜索的位置
* repeat()：返回一个新字符串，表示将源字符串重复n次
* 

## 数值的扩展

## 函数的扩展

### 函数参数的默认值

* 可以为函数的参数设置默认值，直接在参数上赋值即可；参数变量是默认命名的所以不能用let或const再次声明；使用参数默认值时，函数不能有同名参数；参数默认值不是传值的，而是每次都重新计算默认值表达式的值，也就是说参数默认值是惰性求值的。

```js
let x = 99
function foo(p = x + 1){
	console.log(p);
}
foo()  //100
x = 100;
foo()  //101
foo()  //101
```

也就是说每次调用会重新计算，而不是默认等于100

* 可以和解构赋值结合起来使用

```js
function foo({x,y=5}){
	console.log(x,y);
}
foo({})  //undefined,5
foo({x:1})  //1,5
foo({x:1,y:2})  //1,2
```

* 通常情况下定义了默认值的参数应该是函数的尾参数。如果非尾部参数设置默认值，这个参数其实不可缺省。也就是说，不设置在尾部，调用时依旧要传值(但传入undefined会启用默认值)
* 函数的length属性：会返回没有指定默认值的参数的个数，如果设置了默认值的参数不是尾参数，length属性也不会记录默认属性及其以后的参数
* 参数默认值的作用域：函数进行声明初始化时，参数会形成一个单独的作用域，等到初始化结束这个作用域会消失

## 数组的扩展

## 对象的扩展

### 属性的简洁表示法

### 属性名表达式

### 方法的name属性

### Object.is()

### Object.assign()

### 属性的可枚举性和遍历

### \__proto__属性

### Object.setPrototypeOf()，Object.getPrototypeOf()

### Object.keys(),Object.values(),Object.entires()类似于数组实例的方法

### 对象扩展运算符

### Object.getOwnPropertyDescriptors()



## Symbol

ES5的对象属性名都是字符串，容易造成属性名的冲突。Symbol类型表示独一无二的值。通过Symbol函数生成。

```javascript
var s1 = Symbol('foo')
```

* Symbol函数前不能使用new命令，否则会报错，因为Symbol是一个原始类型是直而不是对象
* Symbol函数可以接受一个字符串作为参数，表示对Symbol实例的描述
* 如果Symbol的值是一个对象，就会调用对象 toSting方法将其转为字符串然后才生成一个Symbol值
* Symbol可以显示转换为字符串，布尔值，但是不能转换为数值
* 每一个Symbol值都是不相等的，所以可以作为标识符用于对象的属性名，保证不会出现同名的属性。这对于一个对象由多个模块构成的情况非常有用，能防止某一个键不小心被改写或覆盖。在对象属性名中使用Symbol有以下三种写法

```javascript
var a = {};
a[mySymbol] = 'Hello!'

var a = {
    [mySymbol]:'Hello!'
}

var a = {};
Object.defineProperty(a,mySymbol,{value:'Hello!'})
```

* Symbol值作为对象属性名时不能使用点运算符。因为点运算符后面总是字符串，所以会导致某属性的属性名是字符串而不是Symbol值，这样使用方括号内的Symbol值就无法访问到了
* 通过Symbol值还可以保证switch语句按照设计的方式工作
* Object.getOwnPropertySymbols()方法返回一个数组，成员是当前对象所有用作属性名的Symbol值。
* Symbol.for()接受一个字符串作为参数，然后搜索有没有以该参数作为名称的Symbol值，如果有则返回这个Symbol值，如果没有就新建并返回一个以该字符串为名称的Symbol值。可就是说这个方法可以重新使用一个Symbol值。Symbol()与Symbol.for()都会生成新的Symbol，两者的区别在于前者调用后会直接创建一个新的值，而后者则会搜索全局环境是否存在给定的key，存在则使用，不存在则创建。

```javascript
var s1 = Symbol.for('foo')
var s2 = Symbol.for('foo')
s1 === s2
```

* Symbol.keyFor()返回一个已登记的Symbol值的key。使用Symbol()创建的不会在全局环境中进行登记。而使用Symbol.for()创建的会进行登记
* 内置的Symbol值，指向语言内部使用的方法
  * Symbol.hasInstance
  * Symbol.isConcatSpreadable
  * Symbol.species
  * Symbol.match
  * Symbol.replace
  * Symbol.search
  * Symbol.split
  * Symbol.iterator
  * Symbol.toPrimitive
  * Symbol.toStringTag
  * Symbol.unscopables



## Set和Map数据结构

## Set

类似于数组，但是成员都是唯一的，没有重复

```javascript
const s = new Set();
[2,4,5,6,5,2,2,7].forEach(x => s.add(x));
for(let i of s){
	console.log(i);
}
// 2,4,5,6,7

const set = new Set([1,2,3,4,4]);
[...set]  //[1,2,3,4]

function divs(){
	return [...document.querySelectorAll('div')]
}
const set = new Set(divs());
//类似于
divs().forEach(div => set.add(div))

function dedepe (array) {
	retuen Array.from(new Set(array));
}

let set = new Set('a','b','c')
for(let item of set.entries()){
	console.log(item);
	// ['a','a']
	// ['b','b']
	// ['c','c']
}

```

* 可以接受一个数组(或者具有iterable接口的其他数据结构)作为参数，用来初始化
* 向Set加入值时不会发生类型转换，所以"5"和5是两个不同的值，在Set中NaN等于自身，精确相等运算符===    NaN不等于自身

#### 实例属性与方法，遍历操作

### WeakSet

结构与Set类似，也是不重复的值的集合。

* 与Set的区别：WeakSet的成员只能是对象，而不能是其他类型的值
* WeakSet中的对象都是弱引用，即垃圾回收机制不考虑WeakSet对该对象的引用。也就是说如果其他对象都不再引用该对象，垃圾回收机制会自动回收该对象所用的内存。因此WeakSet适合临时存放一组对象以及更对象绑定的信息。只要这些对象在外部消失，它在WeakSet里的引用就会自动消失
* WeakSet不可遍历，因为他内部有多少个成员取决于垃圾回收机制有没有运行。
* 不适合引用，因为他会随时消失

```javascript
//创建WeakSet数据结构
const ws = new WeakSet()
//可以接受一个数组或类似数组的对象作为参数
const a = [[1,2],[3,4]]
const ws = new WeakSet(a)
```

* 方法
  * add(value)
  * delete(value)
  * has(value)
* 用处：
  * 储存DOM节点，不用担心这些文档从文档流中移除时会发生内存泄露

## Map

JavaScript的对象本质是键值对的集合(Hash结构)，但是只能用字符串作为键。Map类似于对象也是键值对的集合，但是键的范围不限于字符串，各种类型的值都可以当做键。也就是说Object结构实现了字符串-值，Map结构实现了值-值的对应

```javascript
const m = new Map();
const o = {p:'Hello World'},
m.set(o,'content')
m.get(o)  //content
m.has(o)
m.delete(o)
//调用了Map结构的set方法，将对象o当做m的一个键

const map = new Map([
	['name','张三']
	['title','Author']
])
//可以接受数组作为参数，成员是一个个键值对的数组
//如果对一个键进行多次赋值，后面的会覆盖前面的
```

* 只有对同一个对象的引用，Map结构才将其视为同一个键。比如将一个数组设为键，若内存地址不一样则无法读取该键的内容。
* 如果map的键是有简单的类型的值，只有两个值严格相等，就视为一个键。包括+0,-0,NaN。虽然NaN不严格等于自身但Map也将其视为同一个键

#### 实例属性与操作遍历方法

### WeakMap

与map结构类似，也用于生成键值对的集合

* 区别：
  * WeakMap只接受对象作为键名(null除外)
  * 键名所指向的对象不计入垃圾回收机制
* 应用：

## Proxy

用于修改某些操作的默认行为，可以理解为在目标对象前架设一个拦截层，外界对该对象的访问必须先通过这层拦截，因此提供了一种机制可以对外界的访问进行过滤和改写。

```javascript
var obj = new Proxy({},{
	get:function(target,key,receiver){
		console.log(`getting ${key}`);
		return Reflect.get(target,key,receiver)
	},
	set:function(target,key,value,receiver){
		console.log(`setting ${key}`);
		return Reflect.set(target,key,value,receiver)
	}
})
//代码对空对象进行了一层拦截，重定义了属性的get和set行为。
obj.count = 1
//setting count
++obj.count
//getting count
//setting count
```

以上代码说明了Proxy重载了点运算符，用自己的定义覆盖了语言原始的定义

* ES6原生提供Proxy构造函数，用于生成Proxy实例

  * var proxy = new Proxy(target, handler)
    * new Proxy()表示生成一个Proxy实例，target参数表示要拦截的目标对象，handler参数也是一个对象，用来定义拦截行为

* ```javascript
  var proxy = new Proxy({},{
      get:function(target,property){
          return 35;
      }
  })
  proxy.time  //35
  proxy.name  //35
  ```

  以上代码配置对象有一个get方法用来拦截对目标对象属性的访问请求，两个参数分别是目标对象和要访问的属性。因为拦截函数总是返回35，所以访问任何属性都返回35.

* 要使Proxy起作用，必须对Proxy实例进行操作，而把不是对目标对象进行操作。如果handler没有设置任何拦截，等同于直接指向原对象

* 实例方法：
  * get()方法用于拦截某个属性的读取操作
  * set()方法用于拦截某个属性的赋值操作
  * apply()方法用于拦截函数调用call,apply操作
  * has()方法用来拦截HasProperty的操作，即判断某个对象是否具有某个属性时，这个方法会生效
  * construct()用于拦截new命令
  * deleteProperty()方法用于拦截delete操作，如果这个方法抛出或者返回错误，当前属性就无法被delete命令删除
  * defineProperty()方法拦截了Object.defineProperty操作
  * getownPropertyDescriptor()
  * getPrototypeOf()
  * isExtensible()
  * ownKeys()
  * preventExtensions()
  * setPrototypeOf()

## Reflect

* 将Object对象的一些明显属于语言内部的方法比如Object.defineproperty放到Reflect对象上。现阶段某方法同时爱Object和Reflect对象上部署，未来的新方法只在Reflect对象上部署。也就是说从Reflect对象上可以获得语言内部的方法
* 修改某些Object方法的返回结果，让其变得更合理，比如Object.defineProperty在无法定义属性时会抛出一个错误，而Reflect则会返回false
* 让Object操作都变成函数行为。某些Object操作是命令式，比如name in obj和delete obj[name]。

## Promise

* 是异步编程的一种解决方案。简单的来说是一个容器，里面保存着某个未来才会结束的事件(通常是一个异步操作)，他是一个对象可以获取异步操作的信息
* 他有两个特点
  * 对象的状态受外界影响，有三种状态分别是Pending(进行中),Fulfilled(已成功),Rejccted(已失败)。只有异步操作可以决定当前是哪一种状态，其他任何操作都无法改变这个状态。
  * 一旦状态不会改变，任何时候都可以得到这个结果。对象状态改变只存在两种结果，分别是从进行中到已成功和进行中到已失败。只要这两种情况发生，状态就凝固了不会再改变而是一直保持这种状态，这时为resolved(已定型)。如果改变已经发生，为Promise对象添加一个回调函数，也能获得该结果。与Event事件的区别在于事件一旦错过再去监听就得不到结果
* 可以将异步操作以同步操作的流程表达出来，避免层层嵌套的回调函数。缺点是无法取消，一旦创建会立即执行；其次如果不设置回调函数，内部抛出的错误不会反应到外部；处于pending状态时，无法知道进行到哪个阶段。

* 使用：通过构造函数生成promise实例，接受一个函数作为参数，函数的两个参数分别为resolve和reject。resolve函数的作用是将promise对象的状态从未完成转换为成功，reject函数的作用是将状态从未完成变为失败，在异步操作失败时调用，并将异步操作的错误作为参数传递出去。
* promise实例生成以后，可以通过then方法指定resolved和rejected状态的回调函数，then接收两个回调函数作为参数，一个是状态变为resolved时调用，另一个是状态变为reject时调用。第二个参数为可选参数

```javascript
//一个简单例子
function timeout(ms){
    return new Promise((resolve,reject) => {
        setTimeout(resolve,ms,'done')
    })
}

timeout(100).then((value) => {
    console.log(value);
})
```

以上代码中，timeout返回一个promise实例，表示一段时间以后才会发生的结果。过了指定时间ms以后，promise实例的状态变为resolved，就会触发then方法返回的回调函数。

* promise新建后会立即执行，then方法指定的回调函数在当前脚本所有同步任务执行完成后才会执行。

### 案例

```javascript
//异步加载图片,加载成功调用resolve，加载失败调用reject
function loadImageAsync(url) {
	return new Promise(function(resolve,reject){
		var image = new Image;
		image.onload = function(){
			resolve(image);
		}
		image.onerror = function(){
			reject(new Error('Could not load'))
		}
	})
}

//promise实现ajax，对于XMLHttpRequest对象的封装，用于发出针对的数据的http请求，并返回一个promise对象
var getJSON = function(url){
	var promise = new Promise(function(resolve,reject){
		var client = new XMLHttpRequest();
		client.open("GET",url);
		client.onreadystatechange = handler;
		client.responseType = "json";
		client.setRequestHeader("Accept","application/json");
		client.send();
		
		function handler(){
			if(this.readyState !== 4){
				return;
			}
			if(this.status === 200){
				resolve(this.response)
			}esle{
				reject(new Error(this.statusText))
			}
		}
	})
	return promise;
}	
getJSON("/post,json").then(function(json){
	console.log(json);
},function(error){
	console.log("出错");
})
```

### Promise的方法

* catch():是then(null,rejection)的别名，用于指定发生错误时的回调函数
* all()：用于将多个Promise实例包装成一个新的promise实例，这样包装起来的实例状态全部变成FullFilled他才会变成FullFilled，只要有一个为rejected，他就会变成rejected，返回第一个变为reject的实例返回值
* race()方法也是将多个promise实例包装成一个，只要包装中的实例有一个率先改变状态，p的状态就会改变，返回值就传递给p的回调函数
* resolve()：将现有对象转为promise对象，若不带人格参数，则直接返回一个resolved状态的对象
* reject()：返回一个promise实例，状态为rejected

















## Iterator和for...of循环

## generator函数的语法

## Generator函数的异步应用

## async函数

* 返回一个promise对象，可以用then方法添加回调函数，函数执行时遇到await就会先返回

```javascript
async function getStockPriceByName (name) {
	var symbol = await getStockSymbol(name);
	var stockPrice = await getStockPrice(symbol)
	return stockPrice
}
getStockPriceByName('goog').then(function(result){
	console.log(result);
})
```

## Class的基本语法

### 简介

可以看做是一个语法糖，可以让对象原型的写法更清晰。

```javascript
function Point(x,y){
	this.x = x;
	this.y = y;
}
Point.prototype.toString = function(){
	return '(' + this.x + this.y + ')'
};
var p = new Point(1,2);
//可以改写成如下形式
class Point{
	constructor(x,y) {
	    this.x = x;
		this.y = y;
	}
	toString(){
		return '(' + this.x + this.y + ')'
	}
}
```

* 类的数据类型就是函数，类的本身指向构造函数。对类直接使用new()命令，和构造函数的用法完全一致。事实上，类的所有方法都定义在类的prototype属性上
* 在类的实例上调用方法，就是调用原型上的方法。
* 由于类的方法都定义在prototype对象上，所以类的新方法可以添加在prototype对象上。Object.assign方法可以方便地一次向类添加多个方法。
* prototype对象的constructor属性直指向“类”的本身
* 类内部定义的所有属性方法都是不可枚举的
* 类的属性名可以采用表达式，使用[]包裹
* 类和模块内部默认使用严格模式

### constructor方法

是类的默认方法，通过new命令生成对象实例时自动调用该方法。一个类必须有constructor方法。如果没有显式定义，一个空的constructor方法会被默认添加

* 类必须使用new来调用，否则会报错。而构造函数不用new也可以执行

### 类的实例和对象

生成实例对象的写法与ES5完全一样，也是使用new命令。如果没有new会报错

* 实例的属性除非显示定义在其本身(j即this对象上)，否则都是定义在原型(即class)上
* 类的实例共享一个原型对象，这意味着可以通过\__proto__属性为类添加方法

### Class表达式

可以使用表达式的形式定义，且通过该形式定义可以写出立即执行的Class

```js
const MyClass = class Me{
	getClassName(){
		return Me.name;
	}
}

let person = new class{
	constructor(name){
		ths.name = name;
	}
	sayName(){
		console.log(this.name);
	}
}('Lucy');
person.sayName();  //张三
```

### 不存在变量提升

不会把变量声明提升到代码头部。

### 私有方法与私有属性，name属性

* 私有方法：ES6不提供私有方法，只能通过变通方法来模拟实现

```js
//在命名上加以区别,以下代码中_bar方法前面的下划线表示这是一个只限于内部使用的私有方法,但类的外部仍可以调用这个方法
class Weight{
	//公有方法
	foo(baz){
		this._bar(baz);
	}
	//私有方法
	_bar(baz){
		return this.snaf = baz
	}
}
//将私有方法移出模块，因为模块内部的所有方法都是对外可见的,foo是公有方法,内部调用了bar.call(this,baz),使得bar实际上成了当前模块的私有方法
class Weight{
	foo(baz){
		bar.call(this,baz)
	}
}
function bar(baz){
	return this.snaf = baz
}
//利用Symbol值的唯一性将私有方法的名字命名为一个Symbol值，以下代码中bar和snaf都是Symbol值，导致第三方无法获取到他们因此达到了私有方法和私有属性的效果
const bar = Symbol('bar')
const snaf = Symbol('snaf')
export default class myClass{
	//公有方法
	foo(baz){
		this[bar](baz);
	}
	//私有方法
	[bar](baz){
		return this[snaf] = baz;
	}
}
```

* 私有属性：添加私有属性的方法是方法在属性名之前，使用#来表示

```js
class Point{
	#x;
	constructor(x = 0){
		#x = +x;//也可写成this.#x
	}
	get x(){ return #x }
	set x(value){ #x = +value }
}
//在Point类之外读取不到这个属性，且私有属性与实例属性是可以同名的            
//私有属性可以指定初始值在构造函数执行时进行初始化
```

### this指向

默认指向类的实例，单独使用可能会报错

```js
class Logger {
	printName(name = 'there'){
		this.print(`Hello ${name}`)
	}
	print(text){
		console.log(text);
	}
}
const logger = new Logger()
const {printName} = logger;
printName()//报错
//单独提取出来使用时this会指向该方法运行时所在的环境，因此找不到print方法而报错
```



### getter和setter

### 静态方法，静态属性，实例属性























## Class的继承

## 修饰器

## Module的语法

## Module的加载实现

