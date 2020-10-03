## Promise

Promise是异步编程的解决方案；是一个构造函数，使用的是他的实例来进行操作，用于封装一个异步操作并可以获取其结果



状态改变：只有这两种改变，一个promise对象只能改变一次，只会有一个结果数据

* pending------resolved
* pending------rejected



Promise的基本流程

* 执行异步操作
  * 成功执行resolved
    * 返回promise对象，状态为resolved
      * 回调.then()返回新的Promise对象
  * 失败执行reject
    * 返回promise对象，状态为reject
      * 回调.then()/.catch()返回新的Promise对象





通过链式调用的方法解决回调地狱，但还是会有回调函数，可以使用async,await

指定回调函数的方式更加灵活：启动异步任务----返回promise对象----给promise对象绑定回调函数（可以在异步任务结束后指定）









## async / await



### async

函数返回值为promise对象

promise对象的结果由async函数执行的返回值决定



### await

await右侧表达式一般为promise对象，但也可以是其他值

如果表达式是promise对象，await返回的是promise成功的值

如果表达式是其他值，直接将此值作为await的返回值



* await函数必须写在async函数中，但async函数中可以没有await
* 如果await的promise失败了就会抛出异常需要通过try...catch来捕获
* 