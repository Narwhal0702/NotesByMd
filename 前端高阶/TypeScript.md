## 基础类型

* 布尔值：boolean
* 数字：number
* 字符串：string
* 数组：数据类型[]  或  Array<数据类型>
* 元组：允许表示一个一直元素数量和类型的数组，各元素的类型不必相同
* 枚举：enum，使用枚举类型可以为一组数值赋予友好的名字
* any：在编程阶段不清楚变量的指定类型，类型可能来自动态的内容，这种情况下不希望类型检查器对这些值进行检查而是直接让他们通过编译阶段的检查。所以使用any类型来标记这些变量
* void：表示没有任何类型，当一个函数没有返回值时，通常会见到其返回值类型是void
* null和undefined：默认情况下是所以类型的子类型
* never：表示用不存在的值的类型。例如never类型是那些总会抛出异常或根本不会有返回值的函数表达式或箭头函数表达式的返回值类型
* object：表示非原始类型

##  接口

typescript的核心原则之一是对值所具有的结构进行类型检查，接口的作用就是这些类型命名和为代码或第三方代码定义契约

案例：

```js
function printLabel(labelledObj: { label: string }) {
  console.log(labelledObj.label);
}

let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);
```

类型检查器会查看printLabel的调用，printLabel有一个参数，并要求这个对象参数有一个名为label类型为string的属性。传入的对象参数实际上会包含很多属性，但编译器只会检查那些必须的属性是否存在，并且其类型是否匹配。

对上面的案例进行重写：

```js
interface LabelledValue {
  label: string;
}
function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}
let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```

LabelledValue接口好比一个名字，用来描述上面例子里的要求。它代表了有一个label属性且类型为string的对象。需要注意的是，这里并不能像其他语言一样，说给printLabel的对象实现了这个接口，只会关注值的外形，只要传入的对象满足上面提到的条件它就是被允许的；类型检查器不会去检查属性的顺序，只要相应的属性存在并且类型是对的就可以。

### 可选属性

接口里的属性不全都是必需的。 有些是只在某些条件下存在，或者根本不存在。在可选属性名字定义的后面加一个?

好处是可以对可能的属性进行预定义，可以捕获引用了不存在的属性时的错误

案例：

```typescript
interface SquareConfig {
  color?: string;
  width?: number;
}

function createSquare(config: SquareConfig): { color: string; area: number } {
  let newSquare = {color: "white", area: 100};
  if (config.clor) {
    // Error: Property 'clor' does not exist on type 'SquareConfig'
    newSquare.color = config.clor;
  }
  if (config.width) {
    newSquare.area = config.width * config.width;
  }
  return newSquare;
}

let mySquare = createSquare({color: "black"});
```

### 只读属性

一些对象属性只能在对象刚刚创建的时候修改其值，可以在属性名前用readonly来指定只读属性，创建之后就不能再改变了 

案例：

```ts
interface Point {
    readonly x: number;
    readonly y: number;
}
```

