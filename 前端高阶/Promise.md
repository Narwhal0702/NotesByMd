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



