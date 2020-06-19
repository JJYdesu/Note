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

