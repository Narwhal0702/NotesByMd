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

## 开发环境以及生产环境代码示例

```javascript
const {resolve} = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.export = {
	entry:['./src/index.js','./src/index.html']
	output:{
		filename: 'built.js',
		path:reslove(__dirname,'build')
	},
	plugins:[
		new HtmlWebpackPlugin({
			template:'./src/index.html'
		})
	],
	mode:'development',
	devServer:{
		contentBase:resolve(__dirname,'build'),
		compress:true,
		port:3000,
		open:true,
		hot:true
	}
}
```

```javas
//生产环境配置
const {resolve} = require('path')
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const OptimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin');
const HtmlWebpackPlugin = require('html-webpack-plugin')
// 定义nodejs环境变量,决定使用browserslist的哪个环境

// 复用loader
	
const commonCssLoader = [
	MiniCssExtractPlugin.loader
	'css-loader',
	{
		// 兼容性处理,需要在package中定义browrslist
		loader:'postcss-loader',
		options:{
			ident:'postcss',
			plugins:() => [
				require('postcss-preset-env')
			]
		}
] 
process.env.NODE_ENV='production'
module.export = {
	entry:'./src/js/index.js',
	output:{
		filename:'js/built.js',
		path:resolve(__dirname,'build')
	},
	module:{
		rules:[
			{
				test:/\.css$/,
				use:[
					...commonCssLoader
					}
				]
			},
			{
				test:/\.less$/,
				use:[
					[...commonCssLoader],
					'less-loader'
					// loader执行顺序从下往上
				]
			},
			// 正常来讲一个文件只能被一个文件处理,当他要被多个loader处理需要注意执行顺序
			// 先执行eslint,再执行babel
			{
				// 在package.json中eslintConfg ---> airbnb
				test:/\.js$/,
				exclude:/node_modules/,
				loader:'eslint-loader',
				enforce:'pre',  //优先执行
				options:{
					fix:true
				}
			},
			{
				test:/\.js$/,
				exclude:/node_modules/,
				loader:'babel-loader',
				options:{
					presets:[
						[
							'@babel/preset-env',
							{
								useBuiltIns:'usage',
								corejs:{version:3},
								targets:{
									chrome:'60',
									firefox:'50'
								}
							}
						]
					]
				}
			},
			{
				test:/\.(jpg|png|gif)$/,
				use:'url-loader',
				options:{
					limit:8*1024,
					name:'[hash:10].[ext]',
					outputPath:'imgs',
					esModule:false
				}
			},
			{
				test:/\.html$/,
				loader:'html-loader'
			},
			{
				exclude:/\.(html|js|css|less|png|jpg|gif)/,
				loader:'file-loader',
				options:{
					name:'[hash:10].[ext]'
			}
		]
	},
	plugins:[
		new MiniCssExtractPlugin({
			filename:'css/built.css'
		}),
		new OptimizeCssAssetsWebpackPlugin(),
		// 用于压缩
		new HtmlWebpackPlugin({
			template:'./src/inde.html',
			minify:{
				collapseWhitespace:true,
				removeComments:true
				
			}
		})
	],
	mode:'production'  //js自动压缩
}
```