# HTML5

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
	</body>
</html>
```

* \<!DOCTYPE>声明必须位于html5文档中的第一行，该标签告知浏览器文档所使用的 HTML 规范。它是一条指令而不是标签，高速浏览器编写页面所用的标记的版本。让浏览器解析器得知用哪个规范来解析文档，如果没有写这个，浏览器会默认开启混杂模式。也就是会向后兼容用低版本去渲染

* 关于HTML5中的一些新特性分别有
  * canvas元素用于画图
  * video和audio分别用于视屏和音频播放
  * 特殊内容元素，如：article,footer,header,nav,section
  * 表单控件，如：calender,date,time,email,url,search



## 浏览器输入url地址到页面渲染的过程

#### 浏览器输入url地址到页面渲染的过程

**1、输入url后客户端发送域名给DNS服务器解析为ip地址，然后将IP地址返回给浏览器**

​	TCP/IP协议根据IP地址进行访问的，所以需要将域名请求为ip地址

**2、客户端根据IP地址连接到Web服务器**

一个HTTP客户端，通常是浏览器，与Web服务器的HTTP端口（HTTP请求默认端口为80）建立一个TCP套接字连接。

**3、三次握手建立TCP连接后发送HTTP请求**

通过TCP套接字，客户端向Web服务器发送一个文本的请求报文，一个请求报文由请求行、请求头部、空行和请求数据4部分组成。

​	**浏览器与服务器的交互过程**

​		1）首先浏览器利用tcp协议通过三次握手与服务器建立连接

　　http请求包括header和body。header中包括请求的方式（get和post）、请求的协议 （http、https、ftp）、请求的地址ip、缓存cookie。body中有请求的内容。

　　2）浏览器根据解析到的IP地址和端口号发起http的get请求.

　　3）服务器接收到http请求之后，开始搜索html页面，并使用http返回响应报文

　　4）若状态码为200显示响应成功，浏览器接收到返回的html页面之后，开始进行页面的渲染

**4、服务器接受到请求并返回HTTP响应报文**

Web服务器解析请求，定位请求资源，然后执行请求分析，查找数据库等操作后并返回一个HTTP响应。服务器将资源复本写到TCP套接字，由客户端读取。一个响应由状态行、响应头部、空行和响应数据4部分组成。

**5、四次挥手释放连接TCP连接**

若connection 模式为close，则服务器主动关闭TCP连接，客户端被动关闭连接，释放TCP连接;

若connection 模式为keepalive，则该连接会保持一段时间，在该时间内可以继续接收请求;

**6、客户端浏览器解析HTML内容**

客户端浏览器首先解析状态行，查看表明请求是否成功的状态代码。然后解析每一个响应头，响应头告知以下为若干字节的HTML文档和文档的字符集。客户端浏览器读取响应数据HTML，根据HTML的语法对其进行格式化，并在浏览器窗口中显示。

​		**浏览器页面渲染过程**

　　1）浏览器根据深度遍历的方式把html节点遍历成dom 树

　　2）将css解析成CSS DOM树

　　3）将dom树和CSS DOM树构造成render树

　　4）JS根据得到的render树 计算所有节点在屏幕中的位置，进行布局（回流）

　　5）遍历render树并调用硬件API绘制所有节点（重绘）



---



## 关于meta中的标签的作用

提供有关页面的元信息，比如针对搜索引擎和更新频度的描述和关键词，也可以定义页面重定向和刷新，描述，最新版本以及为移动端设备添加视口

```html
<HEAD>

//1.基本标签
   <！ - 声明文档使用的字符编码 - >

    <meta charset =“utf-8”/>

      <！ - 优先使用IE最新版本和Chrome - > 
   <meta http-equiv =“X-UA-Compatible”content =“IE = edge，chrome = 1”> 
// 2.SEO优化
    <！ - 页面关键词 - > 
   <meta name =“keywords”content =“个人活动发布，会办app，活动管理，会议管理，社群管理“/> 
   <！ - 页面描述 - > 
   <meta name =”description“content =”发布个人会议，发布公司会议，w我们都可以帮你找到合适的会议地点和参会观众“> 
   <！ - 网页作者 - > 
   <meta name =”author“content =”xin1642868874@163.com“> 
   <！ - 搜索引擎抓取robotterms是一组使用逗号（， ）分割的值，通常有如下几种取值：none，noindex，nofollow，all，index和follow。 - > 
   <meta name =“机器人“content =”索引，按照“> 
   <！ - 页面重定向和刷新 - > 
   <meta http-equiv =”refresh“content =”0; url =“/> 
//3.可选标签
   <！ - 为移动设备添加视口 - > 
   <meta name =“viewport”content =“width = device-width，initial-scale = 1，maximum-scale = 1，minimum-scale = 1，user-scalable = no” “> 
//4. IOS设备
   <！ - 删除默认的苹果工具栏和菜单栏.--> 
   <meta name =”apple-mobile-web-app-capable“content =”yes“> 
   <！ - 添加到主屏后的标题（iOS 6新增） - > 
   <meta name =“apple-mobile-web-app-title”content =“标题”> 
   <！ - 是否启用WebApp全屏模式 - > 
   <meta name = “apple-mobile-web-app-capable”content =“yes”> 
   <！ - 设置状态栏的背景颜色，只有在“apple-mobile-web-app-capable”content =“yes”`时生效，如果设置为默认或黑色，网页内容从状态栏底部开始。如果设置为black-translucent，网页内容充满整个屏幕，顶部会被状态栏遮挡。 - > 
   <！- 禁止数字识自动别为电话号码 - > 
   <meta name =“format-detection”content =“telephone = no”> 
   <！ - 禁止自动自动识别地址 - >
   <meta name =“format-detection”content =“address = no”> 
   <！ - 禁止自动自动识别日期 - > 
   <meta name =“format-detection”content =“date = no”> 
   <！ -禁止自动自动识别电子邮件 - > 
   <meta name =“format-detection”content =“email = no”> 
   iOS图标<link rel =“apple-touch-icon图片自动处理成圆角和高光等效果/ apple- touch-icon-precomposed禁止系统自动添加效果，直接显示设计原图“>：
       <！ - iPhone和iTouch，默认57x57像素，必须有 - >  
       <link rel =”apple-touch-icon-precomposed“href =“/ apple-touch-icon-57x57-precomposed.png”> 
       <！ - iPad，72x72像素，可以没有，但推荐有 - > 
       <link rel =“apple-touch-icon-precomposed”sizes =“ 72x72“href =”/apple-touch-icon-72x72-precomposed.png“> 
       <！ - Retina iPhone和Retina iTouch，114x114像素，可以没有，但推荐有 - >
       <link rel =“apple-touch-icon-precomposed”sizes =“114x114”href =“/ apple-touch-icon-114x114-precomposed.png”> 
     <!--  Pad的启动画面是不包括状态栏区域的。-->
              <！ - iPad竖屏768 x 1004（标准分辨率） - > 
              <link rel =“apple-touch-startup-image”sizes =“768x1004”href =“/ splash-screen-768x1004.png”>  
              < ！ - iPad竖屏1536x2008（Retina） - > 
              <link rel =“apple-touch-startup-image”sizes =“1536x2008”href =“/ splash-screen-1536x2008.png”>  
              <！ - iPad横屏2048x1496（Retina） - >
              <link rel =“apple-touch-startup-image”sizes =“2048x1496”href =“/ splash-screen-2048x1496.png”> 
      <!-- iPhone和iPod touch的启动画面是包含状态栏区域的。-->
              <！ - iPhone / iPod Touch竖屏320x480（标准分辨率） - > 
              <link rel =“apple-touch-startup-image”href =“/ splash-screen-320x480.png“>  
              <！ - iPhone / iPod Touch竖屏640x960（Retina） - > 
              <link rel =”apple-touch-startup-image“sizes =”640x960“href =”/ splash- screen-640x960.png“>  
              <！ - iPhone 5 / iPod Touch 5竖屏640x1136（Retina） - > 
              <link rel =”apple-touch-startup-image“sizes =”640x1136“href =”/ splash- screen-640x1136.png“>  
 <！ - 添加智能App广告条智能应用横幅（iOS 6+ Safari） - > 
 <meta name =”apple-itunes-app“content =”app-id = myAppStoreID，affiliate-data = myAffiliateData，app-argument = myURL“> 
// 5.Android 
   <！ - Android Lollipop中的Chrome 39增加主题颜色元标签，用来控制选项卡颜色.--> 
   <meta name =“theme-color”content =“＃db5945”> 

 Windows 8

   <！ - Windows 8磁贴颜色 - > 
   <meta name =“msapplication-TileColor”content =“＃000”/> 
   <！ - Windows 8磁贴图标 - > 
360浏览器
   <！ - 设置360浏览器渲染模式： webkit为极速内核，ie-comp为IE兼容内核，ie-stand为IE标准内核.--> 
   <meta name =“renderer”content =“webkit”> 
UC浏览器：
   <！ - 设置屏幕方向：portrait为横屏，landscape为竖屏.--> 
   <meta name =“screen-orientation”content =“portrait | landscape”> 
   <！ - 设置全屏 - > 
   <meta name =“full-screen”content =“是“>
   <！ - 设置适应屏幕排版（缩放是否显示滚动条） - > 
    <meta name =“viewport”content =“uc-fitscreen = no | yes”>
   <！ - 排版模式：适合屏幕）及标准模式（标准） - > 
   <meta name =“layoutmode”content =“fitscreen | standard”> 
   <！ - 夜间模式：可以帮助用户在低亮度或黑暗情况下更舒适的进行页面浏览。注意：页面内的frame / iframe中的夜间模式的元不生效.--> 
   <meta name =“nightmode”content =“enable | disable”> 
   <！ - 整页图片强制显示：为了节省流量及加快速度，UC为用户提供了无图模式 - > 
   <meta name =“imagemode”content =“force”> 
   <！ - 开启应用模式：为方便Web应用及游戏开发者设置的综合开关，通过元标签进行指示打开，当进入应用模式时，浏览器将自动调整以下参数： - > 
   
   <meta name =“browsermode”content =“application”> 
QQ浏览器（X5内核）：
   <！ - 设置横屏，竖屏显示，纵横屏，风景竖屏 - > 
  <meta name =“x5-orientation”content =“portrait | landscape”>
  <！ - 设置全屏显示 - > 
  <meta name =“x5-fullscreen”content =“true”> 
  <！ - 开启应用模式 - >
  <meta name =“x5-page-mode”content =“app”> 
其它：
   <！ - 禁止Chrome浏览器中自动提示翻译 - > 
   <meta name =“google”value =“notranslate”> 
   <！ - - 禁止百度转码 - > 
   <meta http-equiv =“Cache-Control”content =“no-siteapp”> 
    <！ - 禁止浏览器从本地计算机的缓存中访问页面内容：这样设定，访问者将无法脱机浏览.--> 
    <meta http-equiv =“Pragma”content =“no-cache”> 
    <！ - 作用是控制状态栏显示样式 - > 
   <meta name =“apple-mobile-web -app-status-bar-style“content =”black-translucent“> 
   <！ - winphone系统a，输入标签被点击时产生的半透明灰色背景怎么去掉 - > 
   <meta name =”msapplication-tap-突出显示“content =”no“> 
   <！ - 用来阻止广告 - >
   <meta http-equiv =“Content-Security-Policy”content =“default-src gap：// ready file：; style-src'self''unsafe-inline'; script-src'unsafe-inline''unsafe- EVAL'“>
   <！ - 是否开启cleartype显示效果 - > 
   <meta http-equiv =“cleartype”content =“on”> 
   < - 指定360浏览器用webkit内核渲染网页 - > 
   <meta name =“force-rendering” content =“webkit”/> 
   <！ - 自定义标签：app版本号说明 - > 
    <meta name =“app-version”content =“1.13.3”> 
   <title>活动报名</ title> 
</ HEAD>
```



---



### noscript标签

浏览器未开启或不支持JavaScript时显示的内容



---





## H5新特性

* 一些语义化标签比如header，footer，nav，section，aside，article等

* 增强了表单元素input，添加了type属性password,email,url,number等

* 新增表单元素datalist元素规定输入域的选项列表，使用input的list属性和datalist的id属性绑定；keygen提供一种验证用户的可靠方法

* 新增的表单属性placeholder，required，min，max

* 新增音频视频video，audio

* location定位

* 本地存储localStorage，sessionStorage

* 新事件onresize，ondrag，onscroll，onmousewheel，onerror等

* websocket











































