## JSTL

JSP标准标签库，使用这些标签可以完成一些逻辑处理，比如循环遍历集合，让代码更加简洁，不再出现JSP脚本穿插的情况。

实际开发中EL和JSTL结合起来使用，JSTL侧重于逻辑处理，EL侧重于展示数据。

如何使用：

1. 要引入两个jar包（jstl.jar和standard.jar），存放在WEB-INF里面。
2. 在JSP页面开始的地方导入JSTL标签。

```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

3. 在需要的地方使用。



 ## 过滤器

Filter

功能：

1. 拦截传入的请求和传出的响应。
2. 修改或以某种方式处理正在客户端和服务端之间交换的数据流。

使用：

与Servlet类似，Filter是Java Web提供的一个接口开发者只需要定义一个类并且实现这个接口即可。

```java
package com.JJY.servlet;

import javax.servlet.*;
import java.io.IOException;

public class CharacterFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void destroy() {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("UTF-8");
        filterChain.doFilter(servletRequest,servletResponse);
    }
}
```

同时要在web.xml中配置

```html
<filter>
    <filter-name>character</filter-name>
    <filter-class>com.JJY.servlet.CharacterFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>character</filter-name>
    <url-pattern>/testFilter</url-pattern>
</filter-mapping>
```

####  Filter的生命周期

当Tomcat启动时，通过反射机制调用Filter的无参构造函数创建实例化对象，同时调用init()实现初始化，doFilter()调用多次，当Tomcat服务关闭的时候，调用destory()来销毁Filter对象。

同时配置多个Filter，Filter的调用顺序是由web.xml中配置顺序来决定的。

使用场景：

1. 屏蔽敏感词
2. 控制资源控制权限

#### 文件上传下载



#### JDBC

体系结构：

- 面向应用的API，给程序员使用。
- 面向数据库的API。

API：

- Driveranager类
- Connection 接口
- Statement接口
- ResultSet接口

使用：

1. 加载数据库驱动，java程序与数据库之间的桥梁。
2. 加载Connection，Java程序与数据库的一次连接。
3. 创建Statement对象，由Connection产生，执行SQL语句。
4. 如果接收到返回值，创建ResultSet对象，保存Statement执行之后所查询到的结果。



