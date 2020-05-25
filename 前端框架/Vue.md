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
* v-model在表单元素上创建双向绑定。修饰符.lazy可以在改变事件之后进行绑定提高性能；,number输入值转为数值类型；.trim去除首尾字符串

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

* 关于模块系统

  * 推荐创建一个 `components` 目录，并将每个组件放置在其各自的文件中。在局部组件注册之前将每个组件放在各自的文件中、

  * 如果使用了Vue CLI3以上的就可以通过require.context全局注册一些基础的组件，代码如下（做了解即可）

  * ```javascript
    const requireComponent = require.context(
      // 其组件目录的相对路径
      './components',
      // 是否查询其子目录
      false,
      // 匹配基础组件文件名的正则表达式
      /Base[A-Z]\w+\.(vue|js)$/
    )
    ```

* #### 关于Prop：向子组件传递数据

  * 可以在组件上定义一些自定义attribute。

  * ```vue
    <blog-post title="My journey with Vue"></blog-post>
    <!-- 动态赋予一个变量的值 -->
    <blog-post v-bind:title="post.title"></blog-post>
    
    <!-- 动态赋予一个复杂表达式的值 -->
    <blog-post
      v-bind:title="post.title + ' by ' + post.author.name"
    ></blog-post>
    
    ```

  * 如果想将一个度UI小爱过你的所有property传入，可以使用不带参数的v-bind取代v-bind:pro-name

  * 可以以对象形式列出prop，这些property的名称和值分别是prop各自的名称和类型

  * 所有的prop都使得其父子prop之间形成了一个单向的向下绑定，父级prop的更新会向下流动到子组件中，但反过来则不行。这样可以防止子组件意外变更父组件的状态。当父组件发生变更时，子组件中的所有prop都会刷新为最新的值。

  * prop验证：可以在props中的值提供一个带有验证需求的对象，而不是一个字符串数组

* #### 自定义事件

  * 事件名不存在任何自动化的大小写转换。而是触发的事件名需要完全匹配监听这个事件所用的名称。也就是自定义事件无需使用短横线分隔

  * ```javascript
    this.$emit('myEvent')
    //触发一个camelCase的事件
    ```

* #### 组件间通信

  * 访问根实例：$root，在每个vue实例的子组件中，可以通过他来进行访问`this.$root.foo`
  * 访问父级组件实例：$parent，可以用来从一个子组件访问父组件的实例。它提供了一种机会，可以在后期随时触达父级组件，以替代将数据以 prop 的方式传入子组件的方式
  * 访问子组件或子元素：可以使用ref为子组件赋予一个id引用，然后在已经定义ref的组件里使用this.$refs.usernameInput

---

* 是可以复用的vue实例，和new Vue接收相同的选项，例如data等，可以当成一个自定义模板来使用。但是他的data必须是一个函数，这样每个实例可以维护一份返回对象的独立拷贝，如果不是这样可能会影响到其他实例。
* 动态组件：在不同组件间切换，需要在component元素上家一个is属性来实现
* 组件通信
  * 通过props向子组件传递数据
    * props是可以在组件上注册的attribute，
  * 监听子组件的事件：父组件可以通过v-on监听子组件实例的任意事件。子组件可以通过$emit方法传入事件名称来触发一个事件
    * 第一个参数为事件名称，传入的第二个参数可以使他抛出特定的值，在父组件监听这个时事件时可以通过$event访问这个值



## vue-router

将组件components映射到router中，然后告诉vue-router在哪里渲染他们

* ### 动态路由匹配

```javascript
const User = {
  template: '<div>User</div>'
}

const router = new VueRouter({
  routes: [
    // 动态路径参数 以冒号开头
    { path: '/user/:id', component: User }
  ]
})
```

一个路径参数使用:标记，当匹配到一个路由时，参数值会被设置到 `this.$route.params`可以在每个组件内使用。

* ### 响应参数的变化

  * 当使用路由参数时，例如从 `/user/foo` 导航到 `/user/bar`，**原来的组件实例会被复用**。因为两个路由都渲染同个组件，比起销毁再创建，复用则显得更加高效。**不过，这也意味着组件的生命周期钩子不会再被调用**。
  * 常规参数只会匹配被 `/` 分隔的 URL 片段中的字符。如果想匹配**任意路径**，我们可以使用通配符 (`*`)：

* ### 嵌套路由

  * 将一个routerview作为出口，渲染最高级路由匹配到的组件。一个被渲染组件同样可以包含自己的嵌套router-view

  需要在嵌套的出口中渲染组件，需要在路由中使用childrenz配置，可以嵌套多层路由

### 路由导航

可以使用router-link创建a标签来实现导航链接，还可以借助router的实例方法

* 可以给某个路由设置名称

#### 路由重定向

在路由中使用redirect将path路径的路由重定向到redirect的路由，参数除了路径也可以是一个命名的路由

通过alias可以给路由起别名，比如a的别名是b，那么访问b时url为ber路由匹配的是a

#### 路由导航守卫

可以通过router.beforeEach注册一个全局前置守卫：当一个导航触发时，全局前置守卫按照创建顺序调用。守卫是异步解析执行，此时导航在所有守卫 resolve 完之前一直处于 **等待中**。

表示路由发生改变，监听路由从哪里跳转到哪里，接收三个参数，to,from,next



---

## 其他

* axios

  * 是一个基于promise的HTTP库，在vue中使用的话需要先进行安装然后将一些文件引入,vue,axios

  * 然后可以将axios挂载到vue的原型对象上，Vue.prototype.$http = axios这样可以，这样每一个vue的组件都可以通过this直接访问到$http

  * ```javascript
    // 为给定 ID 的 user 创建请求
    axios.get('/user?ID=12345')
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      });
    
    // 上面的请求也可以这样做
    axios.get('/user', {
        params: {
          ID: 12345
        }
      })
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      });
    
    ```

  * ```
    axios.post('/user', {
        firstName: 'Fred',
        lastName: 'Flintstone'
      })
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      });
    ```

---

* ### mixin混入：

* 用来开发Vue组件中的可复用功能。一个混入对象可以白喊任意组件选项，当组件使用混入对象时，所有混入对象的选项将被混入进该组件本身的选项

```javascript
// 定义一个混入对象
var myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}

// 定义一个使用混入对象的组件
var Component = Vue.extend({
  mixins: [myMixin]
})

var component = new Component() // => "hello from mixin!"
```

* 当组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”。

  比如，数据对象在内部会进行递归合并，并在发生冲突时以组件数据优先。

```
var mixin = {
  data: function () {
    return {
      message: 'hello',
      foo: 'abc'
    }
  }
}

new Vue({
  mixins: [mixin],
  data: function () {
    return {
      message: 'goodbye',
      bar: 'def'
    }
  },
  created: function () {
    console.log(this.$data)
    // => { message: "goodbye", foo: "abc", bar: "def" }
  }
})
```

* 同名钩子函数将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子**之前**调用
* 混入也可以进行全局注册。使用时格外小心！一旦使用全局混入，它将影响**每一个**之后创建的 Vue 实例。使用恰当时，这可以用来为自定义选项注入处理逻辑。







## 重点回答内容

#### vue中的MVVM模式(Model-View-ModelView)

* vue以数据进行驱动，自身将DOM和数据进行绑定，一旦创建绑定，DOM和数据将保持同步，每当数据发生变化，DOM会跟着变化。ViewModel是Vue的核心，是Vue的一个实例。
* DOMListeners和DataBindings是实现双向绑定的关键。DOMListener监听页面所有View层DOM的变化。当发生变化，Model层的数据随之变化。DataBindings监听Model层到顶数据，当数据发生变化，View层的DOM元素随之变化

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

### vue的生命周期

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
  * mounted：el被创建的vm.$el替换，并且挂载到实例上之后调用该钩子函数。
  * activated：keep-alive组件激活时使用



### 父子组件通信

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