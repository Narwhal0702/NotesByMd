# Vue面试复习内容总结

## 基本使用

* mustache语法的使用实现数据绑定，里面可以使用JavaScript表达式(不包括流程控制语句与声明语句)，可通过v-once实现一次性绑定(当数据改变时，插值处的内容不会更新)。但mustache不能作用在html的attribute属性上，所以要实现属性的绑定需要使用v-bind；
* v-bind(语法糖:)，v-on(语法糖@)。使用方括号括起来的JavaScript表达式可作为v-bind与v-on参数,例`<a v-on:[eventName]="thingName">`。动态参数求出的是一个字符串，异常情况下为null，其中不能使用空格和引号，但可以使用计算属性代替这个表达式。v-on可使用methods中的方法。
* 事件修饰符v-on:clock.eventName：click.stop阻止事件继续传播；submit.prevent提交文件而不重载页面，once只会触发一次。可以通过v-on添加键盘，鼠标响应事件
* 计算属性：计算属性是基于他们的响应式依赖进行缓存的，只有在响应式依赖发生改变时才会重新求值，这是与方法的区别。但比如Data.now就需要使用methods来使用，因为他不是响应式依赖。计算属性默认只有getter，但可以在需要时写一个set； 
* 侦听器：watch来响应数据的变化，当需要在数据变化时执行异步或开销比较大的操作时比较推荐使用这个方法。可以在执行异步操作时限制执行该操作的频率，并在得到最终结果前设置中间态
* 对象语法：可以给v-bind:class=“”传入一个对象，这样可以动态的切换class。也可以绑定一个返回对象的计算属性。也可以传入一个数组，通过三目运算符动态切换；也可以用在组件上
* 绑定内联样式v-bind:style="{}",通常将样式写在data数据中进行绑定而不是直接写在标签中。也可使用数组。
* v-html指令将数据渲染输出成真正的html(容易导致xss攻击；
* 使用key管理可复用的元素：vue通常会复用已有元素而不是从头开始渲染。比如在v-if与v-else中的输入框中输入内容时，切换后数据不会消失
* 列表渲染v-for,基于一个数组来渲染一个列表，指令需要使用item in items（items也可以为一个值作为普通的for循环）的语法来使用。渲染时支持第二个参数index；也可以用of代替in。可以通过v-for遍历一个对象的键和值与索引。v-if和v-for一起使用时v-for的优先级更高，如果要有条件的跳过循环执行，可以将if放在更外层。
* 如果不使用 key，Vue 会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法。而使用 key 时，它会基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。
* v-model在表单元素上创建双向绑定。修饰符.lazy可以在改变事件之后进行绑定提高性能；.number输入值转为数值类型；.trim去除首尾字符串
* 使用v-on绑定事件时如果函数后加入了一个()就获取不到事件参数e，需要手动传入一个$event默认事件参数对象
* v-if和v-for不能一起使用,v-for的优先级更高比v-if先执行
* 使用v-for遍历渲染的数据，如果在控制台直接使用.语法添加对象属性，已经渲染好的列表不会增加列表项；解决这个问题的方法是重新绑定一个增加了这个属性的新对象；使用Vue.set()或VueObj.$set()增加的对象属性可以渲染出来
* v-for中的key作用：当v-for正在更新已经渲染过的元素列表时，会进行复用，如果数据项的顺序被改变，他不会移动dom来匹配数据项的改变，而是进行复用确保在特定索引下显示已被渲染过的每个元素；key的属性只能为string或number。可以提高渲染的性能，使vue不会去改变原有的元素和数据而是创建新的元素把新的数据渲染进去；也可以避免数据混乱的情况出现

## 进阶使用

### :class和:style

##### :class=“{classname:boolean}”  或  :class="[var1,var2...]"

对象写法中键为样式名，值为bool值

数据写法可以将样式名设置为变量名

##### :style="{attrName:value}"

key值需要使用驼峰

#### v-if和v-show

* v-if直接销毁和重建DOM让达到让元素显示和隐藏效果，v-if是惰性的，可能不创建
* v-show通过修改元素的displayCSS属性让其显示或者隐藏，不管开始条件是什么元素都会渲染，改变的只是css

#### \<style scoped>

* CSS只在当前组件中起作用

#### \<keep-alive>

* 包裹动态组件时，会缓存不活动的组件实例，主要用于保留组件状态或避免重新渲染。比如一个列表和详情页，用户经常在两者间切换，这样就可以对列表组使用\<keep-alive>进行包裹，这样用户从详情返回列表时，都能从缓存中快速渲染而不是重新渲染，降低了性能。

#### v-el

提供一个页面上已存在的DOM元素作为Vue实例挂载的目标，可以使CSS选择器，也可以是HTMLElement实例

#### 嵌套路由的实现

* 在VueRouter中的参数中使用children配置，然后将\<router-view>作为的路由的出口，路由匹配到的组件就会渲染在router-view中
* 子路由的出口必须在父路由中，否则子路由无法显示，通过\<router-link  to="url">指定子路由连接地址

### 过滤器

可以用在双哈括号插值和v-bind表达式，应该被添加在JavaScript表达式的尾部，有管道符号|表示

```js
filters: {
  capitalize: function (value) {
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + value.slice(1)
  }
}
```



## 组件

* 组件的注册分为全局注册和局部注册。

  * 全局注册可以用在任何新创建的Vue根实例的模板，但全局注册意味着即使已经不再使用一个组件了，它依然会被包含在最终构建的结果中，会降低性能；

  * 局部注册的组件通过一个JavaScript对象来定义，然后在components选项中定义想要使用的组件。但局部注册的组件在其子组件中不可用。如需使用需要以一定的写法进行引入。

  * ```javascript
    var ComponentA = { /* ... */ }
    var ComponentB = {
      components: {
        'component-a': ComponentA
      },
    }
    //或
    import ComponentA from './ComponentA.vue'
    export default {
      components: {
        ComponentA
      },
    }
    ```

### 关于组件间通信

#### 父组件向子组件传递数据

使用props来声明需要从父组件接收的数据，props的值可以是两种，一种是字符串数组，一种是对象。

```vue
<div id="app">
	<my-component message="来自父组件的数据"></my-component>
</div>
<script>
	Vue.component('my-component',{
		props:['message'],
		template:'<div>{{message}}</div>'
	})
	var app = new Vue({
		el:'#app'
	})
</script>
```

props中声明的数据与组件data函数中return的数据主要区别就是props来自父级，而data中的是组件自己的数据，作用域是组件本身。在组件的自定义标签上直接写该props的名称，如果要传递多个数据，在props数组中天添加项即可。

如果需要传输动态数据，可以使用v-bind绑定props的值

在props中可进行数据验证：例如指定数据的类型，默认值，是否不许传入等，如果props传入的是一个数组或对象，默认值必须是使用一个函数来返回

---

#### 子组件向父组件传递数据

方法1：通过自定义事件。父组件直接在子组件的自定义标签上使用v-on来监听子组件触发的自定义事件。子组件通过$emit()来触发事件，父组件使用$on()来监听子组件的事件

子组件在自定义的事件方法中通过$emit('eventName',this.dataName)将数据传出，第一个参数是自定义事件的名称，之后都是要传出的数据。父组件可以通过v-on:eventName="父组件中获取数据的方法"。从而达到子组件向父组件传递数据的功能



方法2：通过v-model。直接进行数据双向绑定，但须具备以下条件：接收一个value属性，在有新的value时触发事件

#### 组件间通信

* 访问根实例：$root，在每个vue实例的子组件中，可以通过他来进行访问`this.$root.foo`
* 父链：$parent，可以用来从一个子组件访问父组件的实例。它提供了一种机会，可以在后期随时触达父级组件，以替代将数据以 prop 的方式传入子组件的方式。$children父组件可以通过它访问所有子组件。但不建议使用，子组件应该尽量避免依赖父组件的数据，因为这样会造成父子组建的紧耦合。

```vue
this.$parent.message = ''
```

* 访问子组件或子元素：可以使用ref为子组件标签上赋予一个id引用，然后在已经定义ref的组件里使用this.$refs.usernameInput。

```js
this.$refs.comA.message
```

#### 父子组件通信

* 组件化：将一个页面拆分成各个功能块，方便页面的管理和维护

* 父组件传给子组件数据：
  * props
    * 传递给子组件支持的数据类型，对象或数组默认值必须是一个工厂函数，也就是需要用function来返回数据获取数组可以有默认值；可以通过数组定义多个类型；可自定义类型
    * 传递数据时v-bind后面不支持驼峰，需要进行-转换
* 子组件往父组件传递
  * 自定义事件this.$emit('eventNam',)
* 父组件访问子组件对象
  * $children通过数组的下标访问或所有子组件
  * $refs：默认是一个空的对象，需要在使用的组件中添加
* 子组件访问父组件$paent   



## 关于自定义事件

事件名不存在自动的大小写转换，触发事件需要完全匹配监听这个事件所用的名称。

```html
<my-component v-on:my-event="doSomething"></my-component>
```





## Vue组件中的data为什么是一个函数

组件是可复用的Vue实例，一个组件被创建好之后，就可能被用在各个地方，而组件不管被复用了多少次，组件中的data数据都应该是隔离的互不影响。基于这个理念，组件每复用一次，data数据就用该被复制一次，之后当某一处复用的地方组件内data数据被改变时，其他复用地方组件的data数据不受影响。

能实现这个效果是因为data是一个函数返回值的形式，这样就类似于给每个组件实例创建私有空间。所以每一个组件实例可以维护一份被返回对象的独立拷贝。如果改成对象形式，那么复用的组件会共享同一个数据

## vue中的MVVM模式(Model-View-ModelView)

Model层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View代表UI组件，负责将数据模型转化成UI展现出来；ViewModel是一个同步View和Model的对象

* vue以数据进行驱动，自身将DOM和数据进行绑定，一旦创建绑定，DOM和数据将保持同步，每当数据发生变化，DOM会跟着变化。ViewModel是Vue的核心，是Vue的一个实例。
* DOMListeners和DataBindings是实现双向绑定的关键。DOMListener监听页面所有View层DOM的变化。当发生变化，Model层的数据随之变化。DataBindings监听Model层到顶数据，当数据发生变化，View层的DOM元素随之变化
* 优点
  * 低耦合：视图可以独立于Model变化和修改，一个ViewModel可以绑定到不同的View上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变
  * 可重用性：可以把一些视图逻辑放在一个ViewModel里，这样可以让很多view重用这段视图逻辑
  * 独立开发：可以将业务逻辑，数据，视图分开开发
  * 可测试：将ViewModel业务逻辑独立出来可测试

## vue的生命周期

一个生命周期由父组件开始，但只有全部子组件完成了这个生命周期，父组件才能完成

* 可分为8个阶段：创建前/后, 载入前/后,更新前/后,销毁前/销毁后

* 开始创建、初始化数据、编译模板、挂载Dom、渲染→更新→渲染、销毁等一系列过程，我们称这是Vue的生命周期（也就是从创建到销毁的过程）

* 每一个组件的生命周期分为三个阶段：初始化，运行中，销毁

* 流程：new Vue()创建后初始化生命周期，然后会执行beforeCreate钩子函数，这时无法访问到数据和真是的DOM。

* 在这之后开始挂载数据绑定事件，然后开始执行created函数，这时可以使用到数据，在这里更改数据不会触发updated函数，一般在这里获取初始数据

* 编译模板为虚拟dom放到reder函数中准备渲染，然后执行beforeMount钩子函数，在这个函数中虚拟dom已经创建完成，马上就要渲染,在这里也可以更改数据，不会触发updated，在这里可以在渲染前最后一次更改数据的机会，不会触发其他的钩子函数，一般可以在这里做初始数据的获取。

* 接下来开始render，渲染出真实dom，然后执行mounted钩子函数，这时可以操作真是DOM

* 当组件或实例的数据更改之后，会立即执行beforeUpdate，然后vue的虚拟dom机制会重新构建虚拟dom与上一次的虚拟dom树利用diff算法进行对比之后重新渲染

* 更新完成后，执行updated，数据已经更改完成，dom也重新render完成，可以操作更新后的虚拟dom

* 组件的数据绑定、监听...去掉后只剩下dom空壳，这个时候，执行destroyed

* ##### 常用的生命周期钩子函数

  * created：实例已经创建完成之后调用
  * mounted：el被创建的vm.$el替换，并且挂载到实例上之后调用该钩子函数；ajax异步获取数据会放在最后，所以放在mounted之前都没有用
  * activated：keep-alive组件激活时使用
  * beforeDestory：解绑自定义事件$event.$off；清除定时器；解除自定义dom事件比如window.scroll等

* 

## hash和history的区别

最直观的区别是url中hash模式带了一个#

前端路由的核心就在于改变视图的同时不会向后端发出请求

### hash

hash虽然出现在url中，但不会被包括在HTTP请求中，对后端完全没有影响，因此hash不会重新加载页面

#后面的部分就是hash部分，hash的变化会触发网页跳转，就是可以使浏览器前进后退，但是hash变化不会刷新页面，而且hash不会提交到服务端

hash变化可能的三种原因：js修改，手动修改，浏览器前进后退

hash的变化会触发window.onhashchange事件，并且可以传入事件event获取新旧url，也可以通过location对象获取当前url的hash值

### history

利用了html5 history interface中新增的pushState()和replaceState()方法，这两个方法应用于浏览器中的历史记录栈，在当前已有back，forward，go的基础上，他们提供了对浏览记录进行修改的功能，只是他们执行修改时，虽然改变了当前url，但浏览器不会立即发送后端请求

hash模式下，仅仅hash符号之前的内容会被包含在请求中。因此对于后端来说即使没有做到对路由的全覆盖，也不会返回404错误

history模式下，前端的url必须和实际向后端发起请求的url一致

需要服务端配合，在切换路由时可以携带一些数据进行SEO优化

history模式跳转路由和hash一样不会刷新页面：实现方式和hash不同

* history.pushState()：使用这个api修改url，浏览器不会刷新页面
* window.onpopstate事件：监听浏览器前进后退引起url的改变







## $nextTick()

Vue是一个异步渲染的框架，为了尽量减少dom操作，所以一个函数在data改变后，dom不会立刻去渲染，他会延迟等待多次修改data操作合并成一次再去执行。所以不能再data改变后在同一个函数内立刻去获取dom元素并操作dom元素。如果一定要操作dom元素需要使用$nextTick()

$nextTick(callback)的异步回调函数在DOM渲染之后才被触发，以获取最新的DOM节点，所以在更新数据之后，如果要拿到dom的元素并操作，需要将操作dom部分的代码放入$nextTick的回调函数，这样dom渲染完成后就会去执行操作dom的代码。

```js
method() {
	addItem() {
		this.list.push('abc')
        this.list.push('123')
		// 每次触发就往data里的list中加一项，与数据双向绑定的ul就会多一个li
		// 但数据改变dom不会立刻更新，就去操作ul输出有几个li，输出的是dom更新之前的li个数
		// const ulEle = this.$refs.ulbox
		// console.log(ulEle.childNodes.length)      
        //放进this.$nextTick的回调中就可以等dom渲染完后才执行这段代码
		this.$nextTick(() => {
		   const ulEle = this.$refs.ulbox
		   console.log(ulEle.childNodes.length)
		})
	}
}
```



## computed和watch

computed依赖于缓存进行，不会像调用方法一样重新计算一个值

* 主要用来监听自己定义的变量，该变量不在data里面声明而是直接在computed里面定义，然后就可以当作一个属性在页面上进行双向数据绑定展示出结果或用作其他处理
* computed比较适合对多个变量或对象进行处理后返回一个结果值，也就是多个变量中的某一个值发生了变化监控的这个值也发生变化的情况，就比如购物车的总金额和单个商品数量的变化

watch在监听复杂数据时需要使用深度监听deep，因为vue不监控数组和对象的改变，所以需要在监听的属性内设置deep值并设为true`deep:true`

* watch主要用于监控vue实例的变化，监控的变量必须在data里面声明才可以，一次只能监控单个变量
* 一般用于监听路由，input输入框等特殊的值，比较适合的情况是一个值影响多个数据



## 模板编译的原理

template类似于html但不是html，相比于html他多了指令插值表达式等诸多特性。所以他就是将一种类似于html的代码转化为了某种js代码来完成这种操作这就叫模板编译

使用ljs中的with(obj){}语法，作用是把作用域内的自由变量当做Object属性来查找，如果Object找那个找不到对应的属性不会反悔undefined而是会报错







## 响应式原理

当把一个普通的JavaScript对象传入vue实例中作为data选项，Vue将遍历该对象的所有property，并使用Object.defineProperty将这些property全部转为getter/setter

这些getter和setter对用户来说是不可见的，但是内部他们能让vue追踪依赖，在property被访问和修改的时候通知变更。

每个组件的实例都对应一个watcher实例，他在组件渲染的过程中把接触过的数据property记录为依赖，之后当依赖项的setter触发时，会通知watcher，从而使它关联的组件重新渲染

* 注：不能检测数组和对象的变化

  * 对于对象：vue无法检测property的添加或移除，由于Vue会在初始化实例时对property进行getter/setter转化，所以property必须在data对象上存在才能转换为响应式的；对于已经创建的实例，Vue 不允许动态添加根级别的响应式 property。但是，可以使用 `Vue.set(object, propertyName, value)` 方法向嵌套对象添加响应式 property，还可以使用 `vm.$set` 实例方法，这也是全局 `Vue.set` 方法的别名

  * 对于数组：

    ```js
    //以下两种方式都可以实现和 vm.items[indexOfItem] = newValue 相同的效果，同时也将在响应式系统内触发状态更新
    // Vue.set
    Vue.set(vm.items, indexOfItem, newValue)
    vm.items.splice(indexOfItem, 1, newValue)
    //也可以使用 vm.$set 实例方法，该方法是全局方法 Vue.set 的一个别名
    vm.$set(vm.items, indexOfItem, newValue)
    ```

---

## 数据双向绑定

Vue2.x的数据绑定原理是通过Object.defineProperty()实现，采用了数据劫持结合发布-订阅者模式来劫持各个属性的setter和getter，在数据变动时发布消息给订阅者，触发响应的监听回调。当把一个普通的JavaScript对象传给Vue实例来作为它的data选项时，Vue将遍历它的属性，用Object.defineProperty将他们转为getter或setter。用户看不见getter/setter，但在内部它们让vue追踪依赖，在属性被访问和修改时通知变化

要实现MVVM模式的双向绑定需要实现以下几点

* 实现一个数据监听器Observer，能够对数据对象的所有属性进行监听，如果有变动就可以拿到最新的值并通知订阅者
* 实现一个指令解析器Compile，对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数
* 实现一个Watcher，作为连接Observer和Compile的桥梁，能够订阅并收到每个属性变化的通知，执行指令绑定的响应回调函数，从而更新视图

Vue3以上的版本使用了Proxy来进行监听

Object.defineProperty有以下缺点

* 不能监听数组变化，proxy可以原生支持监听数组
* 要配合Object.keys遍历对象必须遍历对象的每一个属性
* 必须深层遍历嵌套的对象，这样就会造成性能的消耗

### 数据劫持与发布订阅

数据驱动视图的第一步就是数据劫持到data数据的更新，然后再使用发布订阅模式触发视图的更新。核心api是Object.defineProperty。Vue3使用的是proxy但有一定的兼容性问题

###  defineProperty数据监听的使用

`Object.defineProperty(obj,"属性名",属性值)`

```js
const data = {}
const name = 'wtw'
Object.defineProperty(data,"name",{
	get:function(){
		console.log('getter');
		return name
	},
	set:function(newVal){
		console.log('setter');
		name = newVal
	}
})
```

只有Object.defineProperty不能实现数据劫持

```js
//更新视图函数
function updateView(){
	console.log('视图更新');
	dep.notify() // 触发发布订阅模式的更新通知
}
//对对象属性进行递归监听并设置getter与setter
function defineReactive(target,key,value){
	// 递归进行对象的深度监听
	observer(value);
	Object.defineProperty(target,key,{
		get(){
			return value
		},
		set(newVal){
			if(newVal !== value){
				observer(newVal)
				value = newVal;
				updateView();
			}
		}
	})
}
//重定义数组原型用来监听数组操作
const oldArrayProperty = Array.prototype;
//创建新对象,原型指向oldArrayProperty
const arrProto = Object.create(oldArrayProperty)
//监听以下方法对数组的操作
['push', 'pop', 'shift', 'unshift', 'splice'].forEach(methodName => {
  arrProto[methodName] = function () {
    updateView() // 更新视图
    oldArrayProperty[methodName].call(this, ...arguments)
  }
})
//监听对象属性
function observer(target){
	if(typeof target !== 'object' || target === null){
		//不是数组或对象就不进行监听
		return target;
	}
	if(Array.isArray(target)){
		target.__proto__ = arrProto;
	}
	for(let key in target){
		defineReactive(target,key,target[key])
	}
}
class Dep{
	constructor(){
		this.subs=[]//订阅者数组
	},
	addSub(wather){ // 将订阅者加入订阅数组
		this.subs.push(wather)
	},
	notify(){ // 通知订阅者数据更新了，调用自己的update方法更新
		this.subs.forEach(item=>{
				item.update()
		})
	}
}

class Watcher{
	constructor(elementName){
		this.elementName = elementName
	}
	// 订阅者主动进行数据更新
	updata(){
		console.log(this.elementName +'组件要update')
		// 在这里更新组件的dom
	}
}
const dep = new Dep()

// 对三个元素分别进行订阅
const watcher1 = new Watcher('元素1')
dep.addSub(watcher1)
const watcher2 = new Watcher('元素2')
dep.addSub(watcher2)
const watcher3 = new Watcher('元素3')
dep.addSub(watcher3)
```

#### 缺点：

* 深度监听消耗计算大，需要一次就递归到最后一层对象；Proxy分多次递归，用到该属性时才会递归到那里
* 数组也不能直接被监听需要重写数组原型，对原型上的方法特殊处理后才能进行监听
* 直接使用点方法和delete方法进行增加和删除无法被直接监听到，Vue中需要使用`Vue.set`和`Vue.delete`来操作

### Proxy数据监听的使用

除了get和set外还可以删除属性，无需调用Vue.set就可以监听到新增的属性

```js

```



### vue实现数据绑定的原理

* 实现数据绑定主要是实现两个方面的功能：数据导致视图变化，视图变化导致数据变化。后者就是监听视图的事件，然后唉回调函数中改变数据。终重点是数据变化时如何改变视图
  * 思路：通过object.defineProperty()来对数据的属性设置一个set函数，设置后当数据改变时set函数就会被调用，我们就可以里面进行视图更新操作。

### 关于defineProperty的缺陷，以及怎么解决这个问题

使用Proxy解决该问题

* 修改属性默认的特性，该方法接收三个参数，分别是属性所在的对象，属性的名字和一个描述符对象。描述符对象的属性必须是configurable,enumerable,writable和value。设置其中的一个或多个值，可以修改对应的特性值
* 把configurable属性设为false，表示不能从对象中删除属性。如果对这个属性调用delete，在严格模式下回导致错误。一旦把属性定义为不可配置的，就不能把它再变回可配置了。此时再调用该方法修改writable之外的特性都会导致错误
* 他的缺陷：
  * Object.defineProperty无法监控到数组下标的变化，导致通过数组下标添加元素，不能实时响应；
  * Object.defineProperty只能劫持对象的属性，从而需要对每个对象，每个属性进行遍历，如果，属性值是对象，还需要深度遍历。Proxy可以劫持整个对象，并返回一个新的对象。
  * Proxy不仅可以代理对象，还可以代理数组。还可以代理动态增加的属性。
* 有关于vue
  * vue3.0之前的版本都是使用该方法来实现数据的响应式，通过设定对象属性getter/setter方法来监听数据的变化，同时getter也用于依赖收集，而setter在数据变更时通知订阅者更新视图
  * 缺陷：
    * 无法检测到对象属性的新增或删除：由于js的动态性，可以为对象追加新的属性或者删除其中某个属性，这点对经过Object.defineProperty方法建立的响应式对象来说，只能追踪对象已有数据是否被修改，无法追踪新增属性和删除属性，这就需要另外处理
    * 不能监听数组的变化













---





## 关于Vuex

### vuex的工作流程

简单地来说当遇到多个组件共享状态时，单向数据流的间接性很容易被破坏。比如多个视图依赖于同一状态，不同视图的行为需要变更同一状态。

可以将组件的共享状态抽取出来，以一个全局单例模式管理。通过定义和隔离状态管理中的各种概念，并通过强制规则维持视图和状态间的独立性，我们的代码将会变得更结构化且易维护。

就是创建一个store，然后通过在Vue组件中访问this.$store。

是一个转为Vue.js应用开发的状态管理模式，采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。把组件的共享状态抽取出来，以一个全局单例模式管理。在这种模式下，我们的组件树构成了一个巨大的“视图”，不管在树的哪个位置，任何组件都能获取状态或者触发行为

### 基本概念

每一个Vuex应用的核心就是store，store基本上就是一个容器，包含着页面中大部分的状态(state)。

它和单纯的全局对象有以下两点不同：

* Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新
* 不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交(commit)mutation。这样使得我们可以方便地跟踪每一个状态的变化

```js
import Vue from 'vue'
import Vuex from 'vuex'

const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})
```

为了在Vue组件中访问this.$store property，需要为Vue实例提供创建好的store。Vuex提供了一个从根组件向所有子组件以store选项的方式注入该store的机制。

### State

在Vue组件中获得Vuex状态。由于Vuex的状态存储是响应式的，从store实例中读取状态最简单的方法就是在计算属性中返回某个状态

```js
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      return store.state.count
    }
  }
}
```

每当store.state.count变化的时候，都会重新求取计算属性，并触发更新相关联的DOM

通过在根实例中注册store选项，该store实例会注入到根组件下所有的子组件中，且子组件能够通过this.$store访问到

* mapState辅助函数：当一个组件需要获取多个状态时，这些状态都声明为计算属性会有些重复和冗余。可以使用mapState辅助函数生成计算属性

```js
// 在单独构建的版本中辅助函数为 Vuex.mapState
import { mapState } from 'vuex'

export default {
  // ...
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```

可以通过对象展开运算符简便写法

### Getter

有时需要从store中的state中派生出一些状态，例如对列表进行过滤并计数。getter就像计算属性一样，getter的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算

```js
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})

store.getters.doneTodos //[{ id: 1, text: '...', done: true }]
```

接收state作为其第一个参数。Getter会暴露为store.getters对象，可以以属性的形式访问这些值。可以接受其他getter作为第二个参数。

可以通过getter返回一个函数，来实现给getter传参。

* mapGetters辅助函数：将store中的getter映射到局部计算属性

```js
import { mapGetters } from 'vuex'
export default {
  // ...
  computed: {
  // 使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}
```

### Mutation

更改Vuex的store中的状态的唯一方法，每个mutation都有一个字符串的事件类型和一个回调函数，这个回调函数就是实际进行状态更改的地方，并且会接收state作为第一个参数。

```js
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // 变更状态
      state.count++
    }
  }
})
store.commit('increment')
```

提交载荷：可以向store.commit传入额外的参数，即mutation的载荷。多情况下载荷应该是一个对象

```js
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
store.commit('increment', {
  amount: 10
})
```

* 提交mutation的另一种方式是直接使用包含type属性的对象

* Mutation需要遵循Vue的响应规则：提前在store中初始化好所需属性，当需要在对象上添加新属性时使用Vue.set(obj,'aaa',123)或者以新对象替换老对象

* 可以使用常量代替mutation事件类型
* mutation必须是同步函数
* 可以在组件中使用this.$store.commit('xxx')提交mutation，或者使用mapMutatios辅助函数将组件中的methods映射为store.commot调用

### Action

Action类似于mutation，不同之处在于Action提交的是mutation，而不是直接更改状态，可以包含任意异步操作

```js
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
    }
  }
})
```

Action通过store.dispatch触发，和mutation的主要区别是可以执行异步操作，而mutation必须同步执行

### Module

将store分割成模块，每个模块拥有自己的state,mutation,action,getter，嵌套模块等

---

## 关于vue-router

是Vuejs的路由管理器。使用组合组件来组成应用程序，将组件映射到路由，然后告诉Vue Router在哪里渲染他们。

基本使用如下案例

```html
<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- 使用 router-link 组件来导航. -->
    <!-- 通过传入 `to` 属性指定链接. -->
    <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <!-- 路由出口 -->
  <!-- 路由匹配到的组件将渲染在这里 -->
  <router-view></router-view>
</div>
```

```js
// 0. 如果使用模块化机制编程，导入Vue和VueRouter，要调用 Vue.use(VueRouter)

// 1. 定义 (路由) 组件。
// 可以从其他文件 import 进来
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. 定义路由
// 每个路由应该映射一个组件。 其中"component" 可以是
// 通过 Vue.extend() 创建的组件构造器，
// 或者，只是一个组件配置对象。
// 我们晚点再讨论嵌套路由。
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

// 3. 创建 router 实例，然后传 `routes` 配置
// 你还可以传别的配置参数, 不过先这么简单着吧。
const router = new VueRouter({
  routes // (缩写) 相当于 routes: routes
})

// 4. 创建和挂载根实例。
// 记得要通过 router 配置参数注入路由，
// 从而让整个应用都有路由功能
const app = new Vue({
  router
}).$mount('#app')
// 现在，应用已经启动了！
```

### 动态路由匹配

把某种模式匹配到的路由，全都映射到同个组件。比如一个组件，他有id不同的用户都需要使用这个组件，这时就可以在路由路径中使用动态路径参数来达到这个效果。

* 使用路径参数 : 标记。当匹配到一个路由时，参数会被设置到this.$router.params，可以在每个组件中使用

响应路由参数：当使用路由参数时原来的组件实例会被复用，这就意味着生命周期函数不会再被调用

### 嵌套路由

\<router-view>是最顶层的出口，渲染最高级路由匹配到的组件，一个渲染组件同样可以包含自己的嵌套\<router-view>

要在嵌套的出口渲染组件，需要在VueRouter参数中使用children配置

### 编程式的导航

除了使用\<router-link>创建a标签来定义导航链接，可以借助router实例的方法通过编写代码来实现

在vue内部，可以通过$router访问路由实例。

* 想要导航到不同的 URL，使用router.push(location,onComplete?,onAbort)。参数是一个字符串或一个描述地址的对象。第二个和第三个参数是回调，会在导航成功完成或终止的的时候进行调用
* router.replace：和router.push很像，唯一不同的是它不会写像history添加新纪录，而是替换掉当前的history记录
* router.go(n)：参数是一个整数，意思是在history记录中前进或后退几步

### 命名路由

通过一个名称来标识一个路由，在routes配置中通过name属性给某个路由添加一个名称

链接到命名路由可以给router-link 的 to属性传一个对象

### 命名视图

作用：同级展示多个视图。需要使用components而不是component，若router-view没有设置名字则默认使用default

### 重定向和别名

重定向：通过routes中配置redirect来完成，可以是路径，命名的路由，也可以是方法返回重定向目标

别名：通过routes中配置alias来完成，比如用户访问a时，url为a而路由匹配的是a的别名b路由

### 路由组件传参

在组件中使用$route会使之与其对应路由形成高度耦合，从而使某些组件只能在特定的url上使用，限制了灵活性。使用props将组件和路由解耦合

```vue
const User = {
  template: '<div>User {{ $route.params.id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User }
  ]
})
```

```vue
const User = {
  props: ['id'],
  template: '<div>User {{ id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User, props: true },

    // 对于包含命名视图的路由，你必须分别为每个命名视图添加 `props` 选项：
    {
      path: '/user/:id',
      components: { default: User, sidebar: Sidebar },
      props: { default: true, sidebar: false }
    }
  ]
})
```

### history模式

vue-router默认hash模式，使用url的hash来模拟一个完整的url

### 导航守卫

导航表示路由正在发生变化，主要通过跳转或取消的方式守卫导航，参数或查询的改变不会触发进入/离开的导航守卫

router.beforeEach：注册全局前置守卫：当一个导航触发时，全局前置守卫按照创建顺序调用。守卫是异步解析执行，导航在所有守卫resolve完成前一直处于等待中

* 每个导航守卫接收3个参数
  * to:Route 即将要进入的目标路由对象
  * from:Route 当前导航正要离开的路由
  * next:Function 一定要调用该方法来resolve这个钩子
    * next()：进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是confirmed(确认的)
    * next(false)：中断当前的导航，如果浏览器的URL改变了，那么URL地址会重置到from路由对应的地址
    * next('/')或next({path:'/'})：跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。可以向next传递任意位置对象
    * next(error)：如果传入的next参数是一个error实例

### 路由元信息

定义路由时可以使用meta字段。一个路由匹配到的所有路由记录会暴露为$route对象，还有在导航守卫中的路由对象的$route.matched数组。因此需要遍历$route.matched来检查路由中记录的meta字段

### 过渡动效

```html
<transition>
  <router-view></router-view>
</transition>
```

以上会为所有路由设置一样的过度效果，如果想让每个组件有各自的过渡效果，可以在各路由组件内使用transition并设置不同的name

### 数据获取

进入某个路由后，需要从服务器获取数据。例如，在渲染用户信息时，你需要从服务器获取用户的数据。我们可以通过两种方式来实现：

* 导航完成之后获取：先完成导航，然后在接下来的组件生命周期钩子中获取数据，在数据获取期间显示加载中之类的提示
* 导航完成之前获取：导航完成之前，在路由进入的守卫中获取数据，在数据获取成功后执行导航

### 滚动行为

使用前端路由，当切换到新路由时，想要页面滚动到顶部或保持原先的滚动位置，vue-router可以自定义路由切换时页面如何滚动

创建Router实例时，可以提供一个scrollBehavior方法：接收to和from路由对象，第三个参数savePosition当且仅当(通过浏览器前进后退按钮触发时才可用)。

### 路由懒加载

当打包构建应用时，JavaScript 包会变得非常大，影响页面加载。如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了。