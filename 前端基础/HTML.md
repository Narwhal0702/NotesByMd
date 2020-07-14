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

* \<!DOCTYPE>声明必须位于html5文档中的第一行，该标签告知浏览器文档所使用的 HTML 规范。它是一条指令而不是标签，高速浏览器编写页面所用的标记的版本。

* 关于HTML5中的一些新特性分别有
  * canvas元素用于画图
  * video和audio分别用于视屏和音频播放
  * 特殊内容元素，如：article,footer,header,nav,section
  * 表单控件，如：calender,date,time,email,url,search
* 常用标签及其重要属性解析
  * \<a>：定义超链接，用于从一个页面连接到另一个页面
    * href=“url”	链接目标的url
  * \<body>：包含文档中的所有内容，文本图片列表等数据一般都写在body标签内
  * \<br/>：换行符。它是一个单标签



### 关于meta中的标签的作用

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

