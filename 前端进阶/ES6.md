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
* 创建一个块级作用域除了普通的函数声明之外就是使用立即调用函数表达式。

### const命令

声明一个只读的常量，一旦声明常量的值不能改变

* 声明时必须立即初始化
* 只在声明的块级作用域内有效，不会进行变量提升，只能在声明后使用
* 本质：并不是变量的值不可改动，而是指向的那个内存地址不得改动。比如为const创建的对象添加属性，这并不会改变他指向的内训地址值，就可以添加成功；如果想将对象冻结，可以使用Object.freeze()方法

let和const声明变量不会挂载到window对象上，也就是不会把window上的一些bom属性之类的覆盖掉



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

### rest参数

...valueName

* rest参数搭配的变量是一个数组，该变量将多余的参数放入其中,所有数组特有的方法都可用于这个变量

### 箭头函数

* 如果箭头函数不需要参数或需要多个参数，就用圆括号代替参数部分
* 可以简化回调函数，也可以和变量解构，rest参数结合使用
* 注意事项
  * 箭头函数内的this对象就是定义时所在的对象，而不是使用时所在的对象
    * 箭头函数没有自己的this，导致内部的this就是外层代码块的this
      箭头函数的arguments变量就是函数foo的arguments变量
      箭头函数没有自己的this，则不能使用apply(),call(),bind()这些方法改变this的指向
  * 不可以当做构造函数，也就是说，不可以使用new命令，否则会抛出一个错误
  * 不可以使用arguments对象，该对象在函数体内不存在。如果要用可以使用rest参数代替
  * 不可以使用yield命令，因为箭头函数不能作为Generator函数
  * 绑定this：ES7提出了函数绑定运算符，该运算符会自动将左边的对象作为上下文环境(即this对象)绑定到右边的函数上
    * foo::bar等同于bar.bind(foo)

## 数组的扩展

### 扩展运算符

将一个数组转为用逗号分隔的参数序列，也就是说可以直接将数组作为参数使用，该运算符主要用于函数调用

应用：

* 合并数组：[...arr1,..arr2,...arr3] == arr1.concat[arr2,arr3]
* 与解构赋值结合：如果扩展运算符用于数组赋值，只能将其放在参数的最后一位，否则会报错
* 函数返回值：JavaScript的函数只能返回一个值，如果需要返回多个值，只能返回数组或对象，扩展运算符解决了这个问题
* 字符串：可以将字符串转换为真正的数组  [...'hello']
* 实现Iterator接口的对象：任何Iterator接口的对象都可以用扩展运算符转为真正的数组
* Map和Set结构，Generator函数都可使用扩展运算符

### Array.from()

用于将两类对象转为真正的数组

* 类似数组的对象。本质是具有length属性。
* 可遍历对象(包括Set和Map)->Iterator接口：扩展运算符也可以将此类型数据结构转换为数组，但扩展运算符无法转换类似数组的对象
* 另一个应用：将字符串转换为数组，然后返回字符串的长度(可以正确处理各种Unicode字符)，可以避免JavaScript将大于\uFFFF的Unicode字符算作连个字符的bug

### Array.of()

用于将一组值转换为数组。主要目的：弥补数组的构造函数Array()的不足。参数个数的不同会导致Array()的行为有差异。可以代替Array()或new Array()，如果没有参数则返回一个空数组

* 1个参数：指定数组的长度
* 不少于2个参数：返回由数组组成的新数组

### 数组实例的copyWithin()

### 数组实例的find()和findIndex()

### 数组实例的fill()

### 数组实例的entries(),keys(),values()

### 数组实例的includes()

### 数组的空位









## 对象的扩展

### 属性的简洁表示法

ES6允许直接写入变量和函数作为对象的属性和方法，允许在对象中只写属性名，不写属性值，这时，属性值等于属性名所代表的的变量。方法也可以简写。CommonJS模块输出变量就非常适合这种写法

### 属性名表达式

用表达式作为属性名，这时要将表达式放在方括号内；例obj['a' + 'bc'] = 123。属性名表达式和简洁表达式法不能同时使用；属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]

### 方法的name属性

函数name属性返回函数名。对象方法也是函数，因此也有name属性；如果对象的方法使用了getter和setter，则name属性不是在该方法上面，而是在该方法属性的描述对象get和set属性上，返回值是方法名前加get和set；

### Object.is()

用来比较两个值是否严格相等，与严格运算符的行为基本一致；不同之处：+0 != 0，NaN等于自身

### Object.assign()

用于将源对象的所有可枚举属性复制到目标对象，第一个参数书目标对象，后面的参数都是源对象；

* 如果目标对象与源对象有同名属性，或对个源对象有同名属性，则后面的属性会覆盖前面的属性；如果只有一个参数，Object.assign会直接返回该参数；
* 如果该参数不是对象，则会先转成对象，然后返回，undefined和null无法转成对象，如果将它们作为参数就会报错；如果非对象参数出现在源对象的位置(即非首参数)，这些参数都会转成对象，如果无法转成对象便会跳过；
* 其他类型的值不在首参数也不会报错，但是除了字符串会以数组的形式复制到目标对象，其他值都不会产生效果；
* 复制的属性是有限的，只复制源对象自身的属性(不复制继承属性)也不复制不可被枚举的属性(enumerable:false)
* 用途：为对象添加属性，为对象添加方法，克隆对象，合并多个对象，为属性指定默认值

### 属性的可枚举性和遍历

对象的每一个属性都有一个描述对象，用于控制该属性的行为，Object.getOwnPropertyDescriptor方法可以获取该属性的描述对象

遍历对象属性的方法：

* for...in：循环遍历对象自身的和继承的可枚举属性(不含Symbol属性)
* Object.keys()：返回一个数组，包括对象自身的(不含继承的)所有可枚举属性(不含Symbol属性)
* Object.getOwnPropertyNames(obj)：返回一个数组，包含对象自身的所有属性(不含Symbol属性,但是包括不可枚举属性)
* Object.getOwnPropertySymbols(obj)：返回一个数组，包含对象自身的所有Symbol属性
* Reflect.ownKeys(obj)：返回一个数组，包含对象自身的所有属性，不管属性名是Symbol还是字符串，也不管是否可枚举



### \__proto__属性

用来读取或设置当前对象的prototype对象，调用的是Object.prototype.\_\_proto\_\_;如果一个对象本身部署了\__proto__属性，则该属性的值就是对象的原型

### Object.setPrototypeOf()

方法作用于\__proto__相同,用来设置一个对象的prototype对象，返回参数对象本身；如果第一个参数不是对象，则会自动转为对象。但是由于返回的还是第一个参数，所以这个操作不会产生任何效果

### Object.getPrototypeOf()

用于读取一个对象的prototype对象；如果参数不是对象，则会被自动转为对象；如果参数是undefined或null，无法转为对象所以会报错

### Object.keys(),Object.values(),Object.entires()类似于数组实例的方法

* Object.keys()：返回一个数组，成员是参数对自身的(不含继承的)所有可遍历(enumerable)属性的键名
* Object.values()：返回一个数组，方法是参数对象自身的(不含继承的)所有可遍历(enumerable)属性的键值。会过滤属性名为Symbol的属性(不遍历该值)；如果方法的参数是一个字符串，则会返回各个字符组成的一个数组；如果参数不是对象，会先将其转为对象，数组和布尔值的包装对象都不会为实例添加非继承属性，所有会返回空数组
  * 首先遍历所有属性名为数值的属性，按照数字排序
  * 其次遍历所有属性名为字符串的属性，按照生成时间排序
  * 最后遍历所有属性名为Symbol值的属性，按照生成时间排序、
* Object.entries()：返回一个数组，成员是参数对象自身的(不含继承的)所有可遍历(enumerable)属性的键值对数组；会过滤属性名为Symbol的属性(不遍历该值)；基本用途是遍历对象的属性，另一用途是将对象转为真正的Map结构

### 对象扩展运算符

对象的解构赋值用于从一个对象取值，相当于将所有可遍历的，但尚未被读取的属性分配到指定的对象上面；扩展运算符用于取出参数对象的所有可遍历属性，并将其复制到当前对象中

### Object.getOwnPropertyDescriptors()

用来返回某个对象属性的描述对象

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

#### 应用场景

* 使用Symbol来作为对象属性名
* 使用Symbol来代替常量
* 使用Symbol来给对象添加同名属性







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

## Generator函数的语法

### 基础概念

是ES6提供的一种异步编程的解决方案。从语法上可以把它理解成一个状态机，封装了多个内部状态。

* 执行Generator函数会返回一个遍历器对象。也就数说Generator除了是状态机，还是一个遍历器对象生成函数，返回的遍历器对象可以依次遍历Generator函数内部的每一个状态
* 形式上是一个普通函数，特征：
  * function命名与函数名之间有一个星号
  * 函数体内部使用yield语句定义不同的内部状态

```js
function* helloWorldGenerator(){
	yield 'hello';
	yield 'world';
	return 'ending';
}
var hw = helloWorldGenerator();
hw.next();//{value:'hello',done:false}
hw.next();//{value:'world',done:false}
hw.next();//{value:'ending',done:true}
hw.next();//{value:undefined,done:true}
```

以上代码定义的Generator函数共有三个状态，调用方法与普通的函数一样，不同的是调用后该函数并不执行，返回的也不是函数的运行结果，而是一个指向内部状态的指针对象；必须调用遍历器对象的next方法，使指针移向下一个状态。也就是说每次调用next方法，内部指针函数就从头部或上一次停下来的地方开始执行，直到遇到下一条yield/return语句为止

* yield语句是暂停执行的标志
* value属性为内部状态的值，done属性是一个布尔值，表示遍历是否结束

### yield表达式与yield*表达式

yield语句是暂停标志，因为遍历器对象只有调用next方法才会遍历下一个内部状态，所以需要有可暂停的执行函数

一个函数只能执行一次return语句，但是可以执行多次yield语句。可以说Generator生成了一系列的值。如果不使用yield语句，这时他就变成了一个暂缓执行函数。

如果用在另一个表达式中，必须放在圆括号里面。

如果在Generator函数内部调用另一个Generator函数，默认情况下是没有结果的。这时候需要用到yield*语句，在一个Generator函数里执行另一个Generator函数

### next方法的参数

### 与Iterator接口的关系，for...of循环

### Generator.prototype.throw与Generator.prototype.return

### 作为对象属性的Generator和Generator函数的this

### Generator与状态机与协程

### 异步操作的同步化表达

### 控制流管理

### 部署Iterator接口

### 作为数据结构























## Generator函数的异步应用

### 异步的概念和回调函数

Promise回顾

Generator函数

Thunk函数

co模块















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
//async表明函数内部有异步操作，调用该函数会立即返回一个promise对象
```

通过比较就会发现，async函数就是将Generator函数的*替换成async，将yield替换成await，对Generator函数的改进体现为以下四点

* 内置执行器：Generator函数执行必须依靠执行器，所以才有了co模块。async函数自带执行器，也就是说async函数的执行与普通函数一样只需一行
* 更好的语义：async表示函数有异步操作，await表示紧跟在后面的表达式需要等待结果。
* 更广的适用性：co模块约定，yield命令后面只能是Thunk函数或Promise对象，而async函数的await命令后面可以是Promise对象和原始类型的值、
* 返回值是Promise：比Generator函数的返回值是Iterator对象方便了许多。可以用then方法指定下一步的操作。async函数完全可以看做由多个异步操作包装成的一个Promise对象，而await命令就是内部then命令的语法糖

```js
function timeout(ms){
	return new Promise((resolve) => {
		setTimeout(resolve,ms)
	})
}
async function asyncPrint(value,ms){
	await timeout(ms)
	console.log(value);
}
asyncPrint('helloworld',50)
//以上代码指定50ms后输出helloworld
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

//解决方法
//1
class Logger {
	constructor() {
		this.printName = this.printName.bind(this)
	}
}
//2
class Logger{
	constructor() {
	    this,printName = (name = 'there') =>{
				this.print(`Hello ${name}`)
			}
	}
}
//3
function selfish(targer){
	const cache = new WeakMap();
	const handler = {
		get(target,key){
			const value = Reflect.get(target,key);
			if(typeof value !== 'function'){
				return value;
			}
			if(!cache.has(value)){
				cache.set(value,value.bind(target));
			}
				return cache.get(value)
		}
	}
	const proxy = new Proxy(target,handler)
	return proxy;
}
const logger = selfish(new Logger)
```



### getter和setter

在类的内部可以使用get和set关键字对某个属性值设置存值函数和取值函数，拦截该属性的存储行为

```js
class MyClass {
	constructor() {
		//...
	}
	get prop(){
		return 'getter'
	}
	set prop(value){
		console.log('setter:'+value);
	}
}
let inst = new MyClass();
inst.prop = 123;  //setter:123
inst.prop;  //'getter'
```

存值函数和取值函数是设置在属性的Descriptor对象上的

### Generator方法，静态方法，静态属性，实例属性

Generator方法：在某个方法之前加上*，就表示该方法是一个Generator函数。

静态方法：类相当于实例的原型，所有在类中定义的方法























## Class的继承

### 简介

可以通过extends关键字实现继承，比ES5通过原型链实现继承更加清晰和方便







## 修饰器

## Module的语法

## Module的加载实现

