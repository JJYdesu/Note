# MVC与MVVM的那些事儿

首先简单来说，MVC和MVVM是软件工程中的一种软件架构模式，他们把一个软件划分为几个单独的组件，通过组件间的交互来完成软件整体的功能，后端程序员对MVC绝对不陌生，而随着前后端分离开发的概念不断发展，前端MVC逐渐出现在人们的眼前，进而也进化出MVVM的模式。本文将以个人的理解来谈谈前端MVC与MVVM的含义以及二者的区别，最后再谈谈在没有前后端分离的时代，模板引擎到底是一个什么概念。

## MVC

MVC模式最早在1978年被提出，是在20世纪80年代被发明出来的一种软件架构。 它是Model-View-Controller的简写，即模型-视图-控制器。

Model(模型)：是应用程序中的数据模型，在后端中M负责对数据进行获取以及存放，也就是对数据库的操作，而在前端，个人对model的理解是通过网络请求向后端获取到的数据。

View(视图)：顾名思义，视图就是负责将数据展示给用户的，也就是我们在页面上看到的一切，在前端开发中，通常指的就是Dom层。

Controller(控制器)：数据层和视图层是需要交互的，这就要通过一个“中介”来实现了，这个中介就是控制器，它负责从视图读取数据，控制用户数据，并向模型发送数据。

<!--图片来源维基百科-->

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200619101744706.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_70#pic_center)

## MVVM

可以看到，MVVM将MVC中的C换成了VM，VM是ViewModel的意思，这是视图模型层，它是View和Model沟通的桥梁，一方面它实现了数据绑定，将Model的改变实时地反应到View中，另一方面它实现了DOM监听，当DOM发生一些事件，比如点击、滚动时，可以监听到，并在需要的情况下改变对应的数据。

<!--图片来源维基百科-->

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200619102537832.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_70#pic_center)

虽然说C换成了VM，但它不是完全取代Controller，而是在MVC的基础上增加了一层VM，弱化了C的概念，使得开发更加高效，结构更加清晰。

这里用Vue的MVVM举一个例子，首先写一个简单的计数器，代码如下：

```html
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
    <h2>{{counter}}</h2>
    <button @click='add'>+1</button>
    <button @click='sub'>-1</button>
  </div>
  <script>
    const vm = new Vue({
      el:'#app',
      data:{
        counter:0
      },
      methods:{
        add(){
          this.counter++
        },
        sub(){
          this.counter--
        }
      }
    })
  </script>
</body>
</html>
```

当我们点击+1按钮，VM就会帮我们执行事件并改变data（即model层）中的相关的值，当model中的值发生改变后，VM又会帮我们将其反馈在页面上，如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200619103758550.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_70#pic_center)

由此可见MVVM解决了MVC中大量的dom操作，提高了页面渲染的性能，提升了用户体验。

## 模板引擎

什么是模板引擎？一开始我查了一些资料后还是对它的概念比较模糊，然后我就从网站的历史作为突破口来了解，以下仅为个人观点，若有错误望之处。

众所周知，一开始做一个网站并没有什么前端后端分的这么清楚，什么访问数据库，页面渲染等等都是由后端完成的，但后来有人觉得这样不行，什么东西都让后端去做，那后端开发人员岂不是累到吐血，再加上当时网速慢，发个请求要等很久，用得又是同步请求，因此导致用户每请求一次页面都要刷新，刷新又要等很久，用户体验极差。

针对这个问题，就有人提出了js异步操作，比如ajax这种，这种操作请求的时候不需要刷新整个页面，用户体验直线上升，再后来，人们觉得js可以干更多的事情，慢慢地就发展成了前后端分离的开发模式了。

在这种模式中，前端用ajax异步请求加载数据并且局部更新页面，后端也不再需要使用后端页面渲染，页面渲染这块就全部交给前端解决。

重点来了，我们知道，在前后端分离普及之前，网站都大多数都是使用的后端渲染，也就是后端使用模板引擎，给模板(页面)填充数据，然后再将其返回给前端进行展示。但是这样的开发方式，对于复杂的网页而已难以维护，现在应该还是比较少用的了。

## 总结

本文主要讲述了一下前端的MVC和MVVM架构模式，加深了自己对这两种模式的理解，同时还借着本次写博客的机会去了解了一下模板引擎的概念，虽然没有深入探讨，但也算是有一个大概的认识了。文章如有错漏，欢迎批评指正，谢谢~！

