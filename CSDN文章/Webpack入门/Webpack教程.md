## 1.Node环境的安装



## 2.Webpack

### 2.1什么是Webpack？

一个模块打包器。

### 2.2Webpack的作用

试想一下，我们在开发一个html文件时候，有时候可能会引用十几个js文件，而有时候因为他们存在依赖关系，顺序不能乱，同时对于ES6等新规范、less和sass等CSS预处理都不能很好解决，而Webpack就是处理这些问题的一个工具。它可以通过一个入口文件（main.js），从这个文件开始找到项目中的所有依赖文件并处理他们，最后打包成一个或多个浏览器可以识别的JavaScript文件。如果要理解Vue-Cli就需要先学习Webpack。

### 2.3Webpack的安装

Webpack可以使用npm安装，打开电脑cmd，输入以下指令全局安装：

```
npm install -g -webpack  //全局安装
npm install --save-dev webpack  //在项目目录里安装
```

安装完可以在C:\Users\Administrator\AppData\Roaming\npm\node_modules下找到webpack文件夹即为安装成功，或者直接在终端输入

```webpack -v
webpack -v
```

查看版本，但此时系统会提示你需要安装webpack-cli，这是因为Webpack从4.0开始，官方将其本身和cli分开来进行管理，进行安全，直接输入yes，或者ctrl+c退出，输入以下命令：

```
npm install -g webpack-cli
```

安装成功后，再查看版本

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200619230211174.png)

此时webpack安装成功。

### 2.4 一个简单的打包例子

首先新建一个项目文件夹，在终端输入``npm init``生成一个package.json文件，然后新建src和dist文件夹，再创建三个文件：

- ```index.html```--放在dist文件夹中
- ```hello.js```--放在src文件夹中
- ```main.js```--放在项目根目录中

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200619233637997.png)

然后在index.html中写入以下代码，用于引入我们打包后的js文件

```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Webpack Project</title>
</head>
<body>
    <div id='root'></div>
    <script src="bundle.js"></script>   <!--这是打包之后的js文件，我们暂时命名为bundle.js-->
</body>
</html>
```

在hello.js中依据CommonJS规范导出一个模块

```js
// hello.js
module.exports = function() {
    let hello = document.createElement('div');
    hello.innerHTML = "Hello Webpack";
    return hello;
  };
```

最后再main.js这个入口文件中引入这个模块

```js
//main.js 
const hello = require('./src/hello');
document.querySelector("#root").appendChild(hello());
```

打包方式有两种，一种是通过命令行打包，另一种是通过配置文件来打包，我们一般采用后者。在项目根目录下新建一个配置文件```webpack.config.js```，然后写入以下配置代码：

```
// webpack.config.js
module.exports = {
  entry: __dirname + "/main.js", // 入口文件
  output: {
      path: __dirname + "/dist", //打包后的文件存放的地方
      filename: "bundle.js"      //打包后输出文件的文件名
  }
}
```

然后，我们只需要在终端运行``webpack``指令，就可以自动地对文件进行打包。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620001535193.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_0)

此时在dist文件夹中会出现一个``bundle.js``，这个就是我们打包后的文件，直接由``index.html``引用即可。

同时，我们还能将其他的webpack操作指令集成起来，就是说通过一个前缀+自定义的操作名来完成对应的操作，可以在package.json中进行如下修改：

```
{
  "name": "myfirstwp",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "webpack", //将段代码改成这样
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^4.43.0"
  }
}
```

然后我们就可以用```npm start```来进行打包了，虽然看上去更加复杂，但到以后项目复杂起来，需要做更多的操作的时候，它的好处就出来了。

### 2.5Webpack构建本地服务器

Webpack提供了一个本地开发服务器，它是基于node.js构建的，是一个单独的组件，因此需要单独安装并配置依赖，步骤如下：

1. npm下载相应的包
```
   npm i webpack-dev-server -D
```

2. 在webpack.config.js进行相关配置

   ```
    devServer:{
       contentBase: "./dist", // 本地服务器所加载文件的目录
       port: "3066",          // 设置端口号
       inline: true,          // 文件修改后实时刷新
       historyApiFallback: true, //不跳转contentBase
     }
   ```

3. 在package.json中添加启动命令

   ```
   "scripts": {
       "build": "webpack",     //这里我把打包改成了build
       "serve": "webpack-dev-server --open"   //主要是配置这里
     },
   ```

   其中``webpack-dev-serve``是启动服务的命令，而``--open``是自动打开浏览器的命令，我们可以通过一个serve命令将两者集成在一起，最后在终端输入``npm run serve``即可查看页面。

### 2.6Loaders

loaders是Webpack十分重要的功能之一，通过不同的loader，webpack可以调用外部的脚本或工具，实现对不同文件的处理，比如可以将less、sass转成css等等。当然loaders也需要单独安装并在``webpack.config.js``中的``modules``配置项下进行配置，包括以下几个方面：

+ ``test``：一个用以匹配loaders所处理文件的拓展名的正则表达式
+ ``loader``：loader的名称
+ ``include/exclude``：手动添加必须要处理的文件或屏蔽不需要处理的文件(可选)
+ ``options``：为loaders提供额外的设置选项(可选)

下面我们以配置css-loader为例：

1. 安装两个包

   ```
   npm i style-loader css-loader -D
   ```

2. 在webpack.config.js添加module配置项

   ```
   module: {
       rules:[
         {
           test:/\.css$/,   //匹配.css结尾的文件
           use:['style-loader','css-loader']  //注意顺序，调用loader是从右往左编译的的
         }
       ]
     }
   ```

3. 在src文件夹下新建css文件夹，并写一个css文件

      ```
      /* hello.css */
      #root{
          font-size: 36px;
          color: red;
      }
      ```

4. 在main.js中引用

   ```
   import './src/css/hello.css';
   ```

5. 重启服务，可以看到样式已改变

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620103710178.png)

至于其他loader用法都大同小异，这里就不一一叙述。

### 2.7Babel

Babel是一个编译JavaScript的平台，他可以帮你使用新的ES规范，如es6、es7等，也可以使用基于JS进行了扩展的语言，比如React的JSX。下面以解析ES6的包为例子：

1. 安装三个包

   ```
   npm i babel-core babel-loader babel-preset-env -D
   ```

2. 在webpack.config.js的module中配置

   ```
    {
           test:/\.js$/, 
           use:{          //use如果有多项配置，可以用这种写法
             loader:"babel-loader",
             options:{
               presets:[
                 "env"
               ]
             }
           },
           exclude:/node_modules/
      }
   ```

3. 此时，重启服务可能会报错，如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620105854932.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_0)

   这是因为官方规定``babel-loader``和``babel``的版本需要一致，因此需要同一版本，输入以下命令进行版本回退：

   ```
   npm i babel-loader@7 babel-core babel-preset-env -D
   ```

   或者更新到最高的版本也行、

   ```
   npm i babel-loader @babel/core @babel/preset-env webpack -D
   ```

   完成后再次重启服务器，成功运行，现在可以支持ES6的语法了。

### 2.8Plugins

plugins是插件，用于扩展Webpack的功能，他与loader不一样，loader是在打包构建的过程中处理源文件的，一次只能处理一个文件，而插件则是在整个构建过程中起作用，下面介绍两个常用的插件的使用。

1. 自动生成html文件插件

   你应该发现了，我们到现在都还是使用一开始建好的``index.html``，并手动引入js，实际上这样做并不可取，因此我们就需要html自动生成。

   首先安装该插件：

   ```
   npm i html-webpack-plugin -D
   ```

   然后对项目的结构进行一些修改：

   + 删除``dist``文件夹

   + 在``src``文件夹中新建index.template.html文件模板
     ```
     <!-- index.template.html -->
     <!DOCTYPE html>
     <html lang="en">
       <head>
         <meta charset="utf-8">
         <title>Here is Template</title>
       </head>
       <body>
         <div id='root'>
         </div>
       </body>
     </html>
     ```
   
   最后在webpack.config.js引入插件，并配置我们的模板。
   
   执行``npm run build``，可以看到自动生成了dist文件夹，里面有``bundle.js``和``index.html``，插件已经帮我们自动生成好了

2. 热更新插件

   我们现在每次修改完代码都需要重启服务器，比较麻烦，而热更新插件可以帮我们在修改代码并保存后自动刷新预览效果，而且这个插件是webpack自带的，因此我们不用安装，只需要引入webpack模块后再配置一下即可。

   ```
   const webpack = require('webpack') //在webpack.config.js引入webpack模块
   ```

   ```
   new webpack.HotModuleReplacementPlugin() //在plugins中配置插件
   ```

   此时启动服务，修改完代码后保存，浏览器就会自动刷新。



