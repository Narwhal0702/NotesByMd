# 关于Webpack的面试

首先webpack是一个前端资源构建工具，他将前端的所有资源恩建作为模块处理，根据模块的依赖关系进行静态分析，打包生成对应的静态资源bundle

* 他有5个核心概念，分别是entry,ouput,loader(modules),Plugins,Mode,作用分别是
  * 指定webpack指示Webpack以哪个文件为入口起点开始打包，分析构建内部依赖图
  * 指示Webpack打包后的资源输出位置，以及如何命名
  * 处理非JavaScript文件(webpack自身值理解JavaScript)
  * 执行更广的任务，范围包括从打包优化和压缩，一直到重定义环境的变量等
  * 指示Webpack使用相对应的模式配置

* 其他的有devServer,社和开发时使用，会进行自动编译，自动打开并刷新浏览器，只在内存中编译打包，不会有任何输出
* 生产环境下的一系列配置
  * css的兼容性处理插件postcss-loader,压缩插件MiniCCssExtractPlugin
  * js语法检查插件eslint-loader,兼容性插件babel-loader。
* 优化插件：
  * HMR，热模块替换。一个模块发生变化只会重新打包这个模块而不是打包所有模块。
  * source-map:提供源代码到构建后代码映射技术(如果构建后代码出错，通过映射关系可以追踪源代码错误)
  * OneOf优化打包的构建速度，之位文件匹配一个loader，不尝试匹配所有loade，提高性能。如果要匹配两个及以上loader，需要loader取出置外
  * 通过缓存提高效率，比如babel缓存和文件资源缓存
  * tree shaking去除无用代码，能缩小代码体积
  * codesplit：在entry中添加另一个入口，输出多个bundle
  * 懒加载：文件需要使用时才加载，预加载，会在使用前提前加载js文件
  * PWA：无网络情况下依旧可以访问部分的资源

















### 基本概念

webpack是一个JavaScript应用程序的静态模块打包工具，当webpack处理应用程序时，会在内部构建一个依赖图。这个依赖图会映射项目所需的每个模块，并生成一个或多个bundle

### 核心概念

#### 入口(entry)

入口指示webpack应该使用哪个模块作为来构建其内部依赖图的开始。进入入口起点后，webpack会找出哪些模块和库是入口起点直接或间接依赖的

```js
entry: './path/to/my/entry/file.js'
```

entry中可以传入的值有字符串，字符串数组和对象。

#### 出口(output)

告诉webpack在哪里输出所创建的bundle，以及如何命名这些文件。在配置中指定一个output字段用来处理这些过程。主要输出文件的默认地址为 ./dist/main.js ，其他文件默认放置在 ./dist 文件中

```js
const path = require('path');
//需要引入nodejs的核心模块path
output: {
  path: path.resolve(__dirname, 'dist'),
  filename: 'my-first-webpack.bundle.js'
}
```

filename作为输出文件的文件名

#### loader

因为webpack只能理解JavaScript和JSON文件。loader能让webpack去处理其他类型的文件，将他们转化为有效的模块，添加到依赖图中，以供应用程序使用。他能够导入任何类型的模块。主要属性：test用于表示出被对用loader进行转换的某个或某些文件，一般是使用一个正则表达式来匹配文件的扩展名从而找到文件；use属性表示进行转换时应该使用哪个loader

```js
module: {
  rules: [
      { test: /\.txt$/, use: 'raw-loader' }
  ]
}
```

#### 插件(plugin)

loader用于转换某些类型的模块，插件可用于执行范围更广的任务，包括打包优化，资源管理，注入环境变量等。使用一个插件需要require()，然后把它添加到plugin数组中，多数插件可以通过option选项自定义。也可以在一个配置文件找那个因不同的目的而多次使用同一个插件，这是需要使用new操作符来创建它的一个实例

```js
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 用于访问内置插件
plugins: [
  new HtmlWebpackPlugin({template: './src/index.html'})
]
```

#### 模式(mode)

通过选择development,production,none中的一个设置为mode参数，可以启用webpack在相应环境下的优化，默认值为production

```js
mode: 'production'
```



#### 浏览器兼容性

支持所有符合ES5标准的浏览器，也就是IE8以上版本，webpack的import()和reqire.ensure()等需要promise。如果要支持旧版本的浏览器需要在使用这些表达式之前，提前加载polyfill



### 模块热替换(HMR)

会在应用程序运行过程中替换，添加或删除模块，而无需重新加载整个页面，主要通过以下几种方式来显著加快开发速度：

* 保留在完全重新加载页面期间丢失的应用程序状态
* 只更新变更内容
* 在源代码中css/js产生修改时，会立刻在浏览器中进行更新





## 性能优化

### HMR-hot module replacement

模块热替换，一个模块发生变化只会重新打包这个模块而不是打包所有模块



### source-map

提供源代码到构建后代码映射技术(如果代码构建后出错，通过映射关系可以追中源代码错误)

### OneOf

优化打包构建速度，只匹配一个loader不尝试所有loader

### 缓存

第二次构建时读取之前的缓存

### tree shaking

去除无用代码，减少代码体积。也就是说他会移除JavaScript上下文中的未引用代码

### code split

在entry中添加另一个入口输出多个bundle

### 懒加载和预加载

懒加载需要使用时才加载，预加载会提前加载js文件

### PWA

渐进式网络开发环境，在无连接状态下仍可以访问部分资源

### 多进程打包

一般给babel使用

### externals

忽略库的打包然后通过cdn引入

### dll

动态链接库，单独打包提供映射关系，告诉webpack哪些库不参加打包，使用时的名称也要改变





























## 视频总结

首先webpack是一个前端资源构建工具，他将前端的所有资源恩建作为模块处理，根据模块的依赖关系进行静态分析，打包生成对应的静态资源bundle

* 他有5个核心概念，分别是entry,ouput,loader(modules),Plugins,Mode,作用分别是
  * 指定webpack指示Webpack以哪个文件为入口起点开始打包，分析构建内部依赖图
  * 指示Webpack打包后的资源输出位置，以及如何命名
  * 处理非JavaScript文件(webpack自身值理解JavaScript)
  * 执行更广的任务，范围包括从打包优化和压缩，一直到重定义环境的变量等
  * 指示Webpack使用相对应的模式配置

* 其他的有devServer,社和开发时使用，会进行自动编译，自动打开并刷新浏览器，只在内存中编译打包，不会有任何输出
* 生产环境下的一系列配置
  * css的兼容性处理插件postcss-loader,压缩插件MiniCCssExtractPlugin
  * js语法检查插件eslint-loader,兼容性插件babel-loader。
* 优化插件：
  * HMR，热模块替换。一个模块发生变化只会重新打包这个模块而不是打包所有模块。
  * source-map:提供源代码到构建后代码映射技术(如果构建后代码出错，通过映射关系可以追踪源代码错误)
  * OneOf优化打包的构建速度，之位文件匹配一个loader，不尝试匹配所有loade，提高性能。如果要匹配两个及以上loader，需要loader取出置外
  * 通过缓存提高效率，比如babel缓存和文件资源缓存
  * tree shaking去除无用代码，能缩小代码体积
  * codesplit：在entry中添加另一个入口，输出多个bundle
  * 懒加载：文件需要使用时才加载，预加载，会在使用前提前加载js文件
  * PWA：无网络情况下依旧可以访问部分的资源

