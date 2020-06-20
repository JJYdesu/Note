# Vue-Cli快速入门教程

## 一、什么是Vue-Cli

vue-cli是vue的脚手架，顾名思义脚手架是可以帮助我们快速搭建项目的工具，而vue-cli则是vue.js+webpack的项目模板。

## 二、Vue-cli和Webpack的关系

webpack是前端资源模块化管理和打包工具，而vue-cli是基于webpack的，可以理解为对webpack进行了一层封装，我们在使用webpack的时候需要自己手动去引入一些插件，手动去搭建项目的目录结构，而vue-cli则自动帮我们完成这些，省去了开发者自己配置的步骤。

## 三、前期准备

你需要先安装好node环境，如果不会，请看这篇教程[node环境的安装](#)。

如果你想更好地理解vue-cli，请先看一下webpack，教程在此[Webpack快速入门](#)。

## 四、安装Vue-cli

在终端使用以下命令进行安装

```
npm install @vue/cli -g
```

等下载完之后，输入以下指令，若出现版本号，则安装成功

```
vue -V   //注意V大写
```

注意：这里指的是vue-cli的版本，不是vue的版本，现在vue主流还是用2的版本。

## 五、Vue-Cli的使用

### 5.1创建项目

vue-cli提供了两种创建项目的方法，一种是通过官方提供的可视化操作创建项目在终端使用``vue ui``指令后就可以在可视化地创建项目了，另一种则是通过命令行的方式来创建，作为一名程序员，当然是使用后者啦~步骤如下：

输入以下命令，回车

```
vue create 项目名      //默认会加入到git管理
vue create 项目名 -n   //如果不想要git管理，可以使用这条指令
```

这里是选择配置的方式，第一个是默认，第二是个手动，我们一般选择手动配置（第二个），方向键上下选择，回车下一步。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620154056101.png)

这里选择需要用到的组件，各个组件的解释如表格。

|               选项                |                         解释                         |
| :-------------------------------: | :--------------------------------------------------: |
|               Babel               | 一种能让浏览器自动识别向后兼容各版本JavaScript的功能 |
|            TypeScript             |               一种.ts后缀兼容js的语法                |
| Progressive Web App（PWA）Support |                    渐进式网络应用                    |
|              Router               |                  vue的路由管理组件                   |
|               Vuex                |                  vue的状态管理组件                   |
|        CSS Pre-processors         |                      CSS预编译                       |
|         Linter/Formatter          |                  代码检验 格式检查                   |
|           Unit Testing            |             单元测试 以开发角度测试代码              |
|            E2E Testing            |              e2e测试 以用户角度测试代码              |

这里我们先暂时选择Babel，Router和Vuex（空格是选中）。

![在这里插入图片描述](https://img-blog.csdnimg.cn/202006201544541.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_70)

这里是问你router是否使用history模式，先选no，后面会说到，不急。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620154809158.png)

这里选择如何存放配置，我们选第一个，独立一个文件放置。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620155150621.png)

最后问你是否保存当前配置，一般选否，因为每个项目的配置都不一样。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620155245346.png)

然后就开始根据你的选择来创建项目了。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620155408278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_0)

等创建完毕后，可以看到目录多出来这些东西。是不是感觉和webpack有点相似呢？

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020062015575215.png)

最后，进入到项目根目录，输入命令启动项目

```
npm run serve
```

点开自己的项目地址，看到这个页面就说明成功啦。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620155956855.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_0)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200620155956898.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDc2NDA0Nw==,size_16,color_FFFFFF,t_0)##

## 5.2项目结构介绍

