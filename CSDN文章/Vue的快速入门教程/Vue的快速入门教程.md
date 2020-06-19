# Vue的快速入门教程

这是一篇关于前端框架vue的介绍以及快速入门教程，本文将从以下三步带你打开vue的大门：前端技术的发展历程，vue的基本介绍以及vue的基本语法的使用，最后教你如何与后台接口进行交互。

##  一、前端发展历程

从互联网发展到今天，就一直有前端和后端的概念，而对于前端，可以大致分为静态页面、ajax、前端MVC和SPA四个阶段，下面将介绍各个阶段的前端特点。

### 1.静态页面阶段

互联网发展的早期，网站的前后端是一体的，用户浏览网页要经历以下几个步骤：

1. 后端接收到浏览器的请求

2. 生成静态页面

3. 将静态页面返回给浏览器

因此，那个时候的网站如果是要提交表单，就需要整个页面进行刷新，用户体验极差。

### 2.AJAX阶段

后来，AJAX技术诞生，改变了前端的开发。他的全称是Asynchronous Javascript And XML，中文意思是异步JavaScript和XML。有了AJAX技术，就可以通过脚本独立向服务器请求数据，拿到数据后交由前端去处理，而不是后端返回整个页面，整个过程中后端只负责提供数据，由此催生出前后端分离的开发模式。

### 3.前端MVC阶段

前端代码有了读写数据、处理数据、生成视图等功能，因此迫切需要辅助工具，方便开发者组织代码，正如后端MVC一样，这导致了前端 MVC 框架的诞生。简单来说就是前端也拥有像后端一样的Model(数据模型)，View(视图)和Controller(控制)，原生的html+js就可以理解为MVC模式，用户操作请求服务端路由，调用对应的控制器来处理，控制器获取数据后将结果返回给前端。而后来又诞生了MVVM模式，即把Controller换成了ViewModel，若用户在视图层修改了数据，ViewModel层也会自动改变数据，而当ViewModel层的数据发生改变时，又可以将数据自动渲染到页面上，实现了视图层和数据模型的自动同步，整个过程不需要开发者手动进行处理，Vue就是MVVM模式的。如下图所示：

![img](https://img-blog.csdn.net/20180307154352565)

### 4.SPA阶段

SPA的全称是Single Page Application，意思是单页面应用。顾名思义就是在一个页面上展示多页面应用程序。用户的浏览器只需要将网页载入一次，然后所有的操作都可以在这张页面上完成。目前，最流行的前端框架 Vue、Angular、React 等等，都属于 SPA 开发框架。

## 二、Vue的基本介绍

### 1.Vue是什么

这里引用官网的介绍，“Vue是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用”。对于初学者，你只要知道他是一款拥有便于上手以及能极大地提高你的开发效率的优点的前端框架就足够了。

### 2.Vue的安装

我们可以通过三种方式引用Vue：

1. 直接通过标签引用：到[官网](https://cn.vuejs.org/v2/guide/installation.html)下载vue.js，然后直接通过script标签引入。

2. 通过CDN引入：

  ```
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  ```

3. 通过npm下载引入：

  ```
  $ npm install vue
  ```

  此方法可在构建项目中使用，本教程由于是入门教程，将采用第一种方式进行vue的安装。

### 3.创建第一个Vue应用

1. 首先，将你下载好的vue.js放在某个地方，然后在你的html文件中在头部通过script标签引入

2. 每个Vue应用都需要通过实例化Vue来实现，语法如下：
  ```js
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="./vue.min.js"></script>
  </head>
  <body>
    <div id="app">
      <h2>{{msg}}</h2>
    </div>
    <script type="text/javascript">
      var vm = new Vue({    //实例化vue
        el:'#app',
        data:{
          msg:'Hello Vue'
        }
      })
    </script>
  </body>
  </html>
  ```
这里可以看到Vue构造器中有一个el参数，它是DOM元素中的id，在上面实例中id为app。可以理解为我们接下来所有的Vue操作都只有在id为app的这个div中生效，在这外面的都不生效。将该文件启动起来，就能看到页面上显示了"Hello Vue"，这样我们的第一个Vue应用就成功启动了。但是你会发现，我们只是在h2标签中写了个花括号和一个msg啊，怎么就显示Hello Vue了呢？不慌，接来下就马上解释。
  
### 4.Vue基本指令的使用

1. 插值表达式

  Vue使用了基于HTML的模板语法，允许开发者声明式地将DOM绑定至底层Vue实例的数据.最基本的就是通过插值表达式来实现，比如上面提到的{{msg}},这就是一个插值表达式，虽然我们在h2标签中没有写任何的东西，但在vue实例中，我们在data中定义了一个msg属性，里面就有"Hello Vue"，这样一来vue就可以自动帮我们渲染到页面对应的位置。
  
2. v-bind

  v-bind可以动态地绑定标签的属性，写法如下：

  ```vue
  v-bind:property="value"   //普通写法
  :property="value"         //简写
  ```

  示例：

  ```vue
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="./vue.min.js"></script>
  </head>
  <body>
    <div id="app"> 
      <h2 v-bind:style="{color:colorObj.red}">直接绑定绑定样式属性</h2>
      <div :class='{classA:is}'>绑定class中判断</div>
      <div :class='[classB,size]'>通过数组绑定多个样式属性</div>
      <div :class='is?classA:classB'>也可以使用三元表达式</div>
    </div>
    <style>
      .classA{
        color: green;
        font-size: 24px;
      }
      .classB{
        color: yellow;
      }
      .size{
        font-size: 36px;
      }
    </style>
    <script type="text/javascript">
      var vm = new Vue({
        el:'#app',
        data:{
          colorObj:{
            red:'red',
            green:'green'
          },
          is:true,
          classA:'classA',
          classB:'classB',
          size:'size'
        }
      })
    </script>
  </body>
  </html>
  ```

  效果如下：

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200618113012742.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_70#pic_center)

3. v-model

  v-model用于创建双向绑定。我们知道Vue的核心特性之一就是双向绑定，我们可以通过v-model这个指令来实现，语法格式如下：

  ```vue
  v-model="attr"
  ```

  该指令通常用在<input>、<select>、<textarea>这些表单标签中使用。示例如下：

  ```vue
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="./vue.min.js"></script>
  </head>
  <body>
    <div id='app'>
      <input type="text" v-model="msg" placeholder="请输入内容">
      <h2>你输入的内容是：{{msg}}</h2>
    </div>
    <script type="text/javascript">
      var vm = new Vue({
        el:'#app',
        data:{
          msg:''
        }
      })
    </script>
  </body>
  </html>
  ```

  用户在input中输入内容的时候，通过v-model可以将内容绑定到data中，再通过插值表达式就可以响应式地反馈在页面上，效果如图：

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200618103018362.png)

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200618103018363.png)

4. v-on

	v-on是用来绑定事件监听的，最常用的当然是点击事件，语法如下：

	```vue
	v-on:click='method'	//基本写法
	@click='method'		//语法糖写法
	```

	示例如下：

	```
	<!DOCTYPE html>
	<html lang="en">
	<head>
	  <meta charset="UTF-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1.0">
	  <title>Document</title>
	  <script src="./vue.min.js"></script>
	</head>
	<body>
	  <div id='app'>
	    <button v-on:click='test'>点我打印</button>
	    <button @click='test2'>语法糖写法</button>
	  </div>
	  <script>
	    var vm = new Vue({
	      el:'#app',
	      data:{
	      },
	      methods:{
	        test(){
	          console.log('这里是v-on：click')
	        },
	        test2(){
	          console.log('这里是@click')
	        }
	      }
	    })
	  </script>
	</body>
	</html>
	```

	通过v-on绑定事件名称后，我们需要在方法属性methods中定义对应的事件即可。

	效果如下：

	![在这里插入图片描述](https://img-blog.csdnimg.cn/20200618104155921.png#pic_center)

5. 条件语句

	Vue提供了一种和普通编程语言一样的条件语句判断，我们可以在标签上使用v-if,v-else-if和v-else来实现条件判断展示元素，当然也可以使用v-show根据值来展示元素。示例如下：

	```vue
	<!DOCTYPE html>
	<html lang="en">
	<head>
	  <meta charset="UTF-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1.0">
	  <title>Document</title>
	  <script src="./vue.min.js"></script>
	</head>
	<body>
	  <div id='app'>
	    <h2 v-if="type==='A'">此时type的值为A</h2>
	    <h2 v-else-if="type==='B'">此时type的值为B</h2>
	    <h2 v-else-if="type==='C'">此时type的值为C</h2>
	    <h2 v-show='ok'>v-show展示元素<h2>
	  </div>
	  <script>
	    var vm = new Vue({
	      el:'#app',
	      data:{
	        type:'B',
	        ok:true
	      },
	    })
	  </script>
	</body>
	</html>
	```

6. 循环语句

	Vue也提供了v-for来循环生成元素，需要使用 **site in sites** 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名。示例如下：

	```
	<!DOCTYPE html>
	<html lang="en">
	<head>
	  <meta charset="UTF-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1.0">
	  <title>Document</title>
	  <script src="./vue.min.js"></script>
	</head>
	<body>
	  <div id='app'>
	    <ul>
	      <li v-for='item in array'>
	        <h2>编号：{{item.id}}</h2>
	        <h2>姓名：{{item.name}}</h2>
	        <h2>年龄：{{item.age}}</h2>
	        <h2>---------------------</h2>
	      </li>
	    </ul>
	  </div>
	  <script>
	    var vm = new Vue({
	      el:'#app',
	      data:{
	        array:[
	          {id:1,name:'小红',age:18},
	          {id:2,name:'小明',age:22},
	          {id:3,name:'小白',age:33},
	        ]
	      }
	    })
	  </script>
	</body>
	</html>
	```

	效果如下：

	![在这里插入图片描述](https://img-blog.csdnimg.cn/20200618110736951.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_70#pic_center)

	当然也可以迭代对象和整数，示例如下：

	```Vue
	<!DOCTYPE html>
	<html lang="en">
	<head>
	  <meta charset="UTF-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1.0">
	  <title>Document</title>
	  <script src="./vue.min.js"></script>
	</head>
	<body>
	  <div id='app'>
	    <ul>
	        <!-- 迭代对象 -->
	      <li v-for='item in obj'>  
	        <h2>{{item}}</h2>
	      </li>
	        <!-- 迭代整数 -->
	      <li v-for='n in 5'>   
	        这是第{{n}}个数
	      </li>
	    </ul>
	  </div>
	  <script>
	    var vm = new Vue({
	      el:'#app',
	      data:{
	        obj:{
	          name:'Jacky',
	          age:22,
	          city:'广州'
	        }
	      }
	    })
	  </script>
	</body>
	</html>
	```

	效果如下：

	![在这里插入图片描述](https://img-blog.csdnimg.cn/20200618111308441.png#pic_center)

7. 计算属性

  经过上面的学习，我们可以看到插值表达式的使用十分方便，除了直接展示data中的数据之外，实际上我们还能在里面进行一些运算，比如：

  ```
  {{msg.split("").reverse().join("")}}
  ```

  像这样复杂的运算都是可以在插值表达式中使用的，但是它的初衷只是用于进行简单的运算，遇到这种复杂运算的话看上去会比较繁琐，不适合在这里使用，而**计算属性computed**则是帮我们处理这种复杂运算的，当然你可能会问，“那我们绑定一个方法来处理这些数据啊”，确实，方法属性也可以达到同样的目的。他们的区别主要在于执行机制的不同：

  + computed里的方法在初始化执行过后，只要任何值有更新，那么所有在computed计算属性里和其相关的值都会更新。
  + methods只有在调用的时候才会执行对应的方法，不会自动同步数据。

  因此，computed是有缓存的，在处理大量数据的时候可以提高效率，如果你不希望缓存，则可以使用methods属性。

  除此之外，二者在内部的函数写起来没有区别，但在调用的时候会不一样，如下所示：

  ```
  <!-- 计算属性里方法的调用，可以看到这里没有括号 -->
  <div id="app">
  	总价： {{ prices }} <br/>
  	test:{{ tests }}
  </div>
  
  <!-- methods里方法的调用，而这里是有括号的 -->
  <div id="app">
  	总价： {{ prices() }} <br/>
  	test:{{ tests() }}
  </div>
  
  ```

  至此，Vue的基本常用指令就讲完了，最后来教一下Vue应用如何与后端接口交互。


### 5.Vue与后端的交互

众所周知，前后端可以通过ajax技术进行交互，而在Vue2.0开始，就推荐使用axios进行网络请求，它对Ajax进行几乎完美的封装，解决了原生ajax许多缺点，同时由于它支持promise，因此不会出现jueryAjax的**回调地狱**。接下来我们就来看看axios怎么使用。

1. 前期准备

	你需要一个后端接口，可以使用mockjs等等来模拟后端接口，我这里则使用nodejs+express框架自己写一个简单的API来测试。

2. 安装

	和Vue一样，你可以通过三种方式来安装，这里我采用的是cdn引入。

	```javascript
	 <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
	```

3. Get请求

	首先是get请求

	```html
	<!DOCTYPE html>
	<html lang="en">
	<head>
	  <meta charset="UTF-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1.0">
	  <title>Document</title>
	  <script src="./vue.min.js"></script>
	  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
	</head>
	<body>
	  <div id='app'>
	    <button @click='test'>发送请求</button>
	  </div>
	  <script>
	    var vm = new Vue({
	      el:'#app',
	      data:{
	      },
	      methods:{
	        test(){
	          axios.get('http://localhost:3038/test?id=0').then(res=>{
	            console.log(res)
	          }).catch(err=>{
	            console.log(err)
	          })
	        }
	      }
	    })
	  </script>
	</body>
	</html>
	```

	在引入了axios的cdn后，就可以在方法中使用了，基本使用如上所示，.get是声明请求的类型,.then则是处理服务端返回的结果，而.catch则是捕获异常。当然url中除了直接拼接参数外，还可以使用params设置参数，比如：

	```javascript
	axios.get('http://localhost:3038/test',{
	            params:{
	              id:2,
	              name:'JJY'
	            }
	          }).then(res=>{
	            console.log(res)
	          }).catch(err=>{
	            console.log(err)
	          })
	```

	请求成功后返回结果打印，同时后台也能拿到相应的参数了：

	![在这里插入图片描述](https://img-blog.csdnimg.cn/2020061814452483.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_70)

	![在这里插入图片描述](https://img-blog.csdnimg.cn/2020061814452485.png)

4. Post请求

	其实Post请求的写法也差不多，这里用传递配置的方式来写。

	首先定义一下请求的各项参数，格式如下：

	```javascript
	var config = {
					method: 'post',
					url: 'http://localhost:3038/post',
					data: {
							name: 'JJY',
							age: 22,
							country: '中国',
							},
					}
	```

	然后将这些配置直接放进axios即可

	```javascript
	axios(config).then((res) => {
									console.log(res)
								})
								.catch((err) => {
									console.log(err)
								})
	```

	请求成功后返回结果打印，同时后台也能拿到相应的参数了：

	![在这里插入图片描述](https://img-blog.csdnimg.cn/20200618152157605.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_70)

  

​                                              ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200618152157601.png#pic_center)

### 6.总结

至此，Vue的入门指南到此结束，本文主要讲述了Vue的一些入门操作，以及如何使用Vue进行前后端的交互，因为是入门级的，因此还没有涉及到vue路由和vuex等，这些打算在日后的vue-cli文章中再进行说明，本文如有错漏欢迎指出，谢谢~

