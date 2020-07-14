# ajax

* 是一种用于创建快速动态网页的技术，通过与服务器的少量数据交换可以让网页实现异步更新，这就是说可以在不重新加载整个网页的情况下对某部分进行更新
* 工作原理：相当于在用户和服务器之间加了—个中间层(AJAX引擎)，使用户操作与服务器响应异步化。并不是所有的用户请求都提交给服务器。像—些数据验证和数据处理等都交给Ajax引擎自己来做,，只有确定需要从服务器读取新数据时再由Ajax引擎代为向服务器提交请求。

### ajax实现

AJAX创建异步对象XMLHttpRequest

操作XMLHttpRequest 对象

（1）设置请求参数（请求方式，请求页面的相对路径，是否异步）

（2）设置回调函数，一个处理服务器响应的函数，使用 onreadystatechange ，类似函数指针

（3）获取异步对象的readyState 属性：该属性存有服务器响应的状态信息。每当 readyState 改变时，onreadystatechange 函数就会被执行。

（4）判断响应报文的状态，若为200说明服务器正常运行并返回响应数据。

（5）读取响应数据，可以通过 responseText 属性来取回由服务器返回的数据。

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'aabb.php', true);
xhr.send(null);
xhr.onreadystatechange = function() {
	if(xhr.readyState==4) {
		if(xhr.status==200) {
			console.log(xhr.responseText);
		}
	}
}
```

* open()设置请求方式和请求地址：参数分别是method请求文件的类型get/post；url为文件在服务器上的位置；async：true为异步false为同步，永远设置为true
* send()发送请求
* onreadystatechange:监听状态变化，其中readyState参数分别为0-4:
  * 请求未初始化
  * 服务器连接已建立
  * 请求已接收
  * 请求处理中
  * 请求已完成且响应已就绪，status返回http状态码

## 官方文档阅读

通过在后台与服务器进行少量数据交换，ajax可以使网页实现异步更新，这意味着可以在不重新加载整个网页的情况下对网页的某部分进行更新，传统的网页需要更新内容必须重载整个页面

关于ajax的实例解释：比如在一个标签上添加一个点击事件调用包含了ajax的方法。

### 使用步骤

创建对象

请求

响应

readyState





































