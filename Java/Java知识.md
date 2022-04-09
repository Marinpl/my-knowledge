# Java相关知识补充

-- 本文应在掌握基本 Java基础知识后，进行阅读，起到查漏补缺之功效。

-- 若需了解java基础知识，请先学习[java基本教程](https://www.runoob.com/java/java-tutorial.html) 或 [观看基础知识视频](https://www.bilibili.com/video/BV12J41137hu?p=1)

## 0. Java

## 1. JVM

​	**什么是JVM？**

​	是一种虚拟机(虚构出来的计算机)，是通过在实际的计算机上仿真模拟各种计算机功能来实现的。使用虚拟机，Java语言在不同平台上运行时不需要重新编译。

## 2. Java SE/ME/EE  和 J2EE 

### 基本概念：

Java SE(Java Platform,Standard Edition)：基础，基于`jDK`和`JRE`包含支持 Java Web 服务开发的类，并为 Java EE和ME提供基础。

Java EE(Java Platform,Enterprise Edition)：企业版本，提供了`JDBC`、`EJB`、`Annotation`、`JB`、`API`、`JPA`、`JMS`等等主要技术。

J2EE(Java 2 Platform Enterprise Edition)：企业版本更新，汇聚了更多技术，是一个企业级的分布式应用程序。

Java ME(Java Platform,Micro Edition)：已基本淘汰。

### J2EE详解：

#### 1. 起源

​	随着基于Java的企业应用呈爆炸式增长。但是各企业系统API之间又不能相互兼容。于是制订了一个基于Java组件技术的企业应用系统开发规范，该规范定义了一个多层企业信息系统的标准平台，旨在简化和规范企业应用系统的开发和部署。

#### 2. J2EE规范

​	J2EE在JavaSE基础上完善了体系，拥有了相对结构【表现层(Struts、JSF等) +应用层(处理业务，可以是JavaBean也可以是EJB) +持久层(JDBC、Hibernate)】，添加了许多新的功能。

规范如下所示图:

​                                                                          	<img src="C:\Users\willa\Desktop\knowledge\J2EE standard.jpg" style="zoom: 33%;" />                            



#### 3. 规范设计技术详解

###### ServLet

​	是服务端的Java应用程序，可以生成动态的页面，在客户端Session中保存客户的数据。它定义了动态生成HTML、XML或其他格式文档的Web网页的技术标准。有8大内置对象。

###### JSP

​	(Java Server Pages)，JSP页面由HTML代码和嵌入其中的Java代码组成。它将网页逻辑与网页设计显示分离，支持可重用的基于组件的设计，使java开发快速、容易。JSP是一种动态页面技术，它主要目的是将表示逻辑从Servlet中分离出来。

###### JDBC

​	(Java Database Connectivity)，创建数据库连接，跟ODBC相似，独立于平台。通常是面向关系型数据库的。

###### XML

​	(Extensible Markup Language)， 是一种可扩展标记语言，XML可以从HTML中分离数据，也可用于交换数据、充分利用数据等。

#### 4. 其他关联：

###### 1-- MVC\ MVP\ MVVM设计模式：

**MVC**：Model-View-Controller

目前由于Model和View之间耦合度过大，添加了Service服务层解耦。

结构图如下图所示：

​		                                                                 <img src="C:\Users\willa\Desktop\Knowledge\MVC frame.jpg" style="zoom: 50%;" />

​	**特点**：

- 具有一定的分层，model彻底解耦，controller和view并没有解耦
- 层与层之间的交互尽量使用回调或者去使用消息机制去完成，尽量避免直接持有
- controller和view在android中无法做到彻底分离，但在代码逻辑层面一定要分清
- 业务逻辑被放置在model层，能够更好的复用和修改增加业务

----



**MVP**：Model-Presentner-View

**MVP**是一种用户界面体系结构模式，旨在促进自动化单元测试和改进显示逻辑中关注点的分离

结构图如下图所示：

<img src="C:\Users\willa\Desktop\knowledge\MVP frame.jpg" style="zoom: 33%;" />

  **特点**：

- Model和View之间不进行通讯
- 通过定义好的接口进行交互
- View只应该有简单的Set/Get的方法
- 创建Adapter访问Model和View
- 一般不容许直接访问Model

----



**MVVM**：Model-ViewModel-View

MVVM是一种主要用于数据展示的结构模式，旨在放置绝大多数逻辑在后端，前端只用把数据展示或交互

结构图如下图所示：

​	                                                                      <img src="C:\Users\willa\Desktop\knowledge\MVVM frame.jpg" style="zoom:50%;" />  

 **特点**：

- 双向绑定结构
- DataBinding



###### 2-- Hibernate：

​	对JDBC进行了非常轻量级的对象封装，通过持久化数据对象，将POJO与数据库表建立映射关系，并以对象的角度来访问数据库。 		          	Hibernate可以应用在任何使用JDBC的场合，既可以在Java的客户端程序使用，也可以在Servlet/JSP的Web应用中使用，方便数据持久化。

###### 3-- Mybatis：

​	是一款持久层框架，支持定制化SQL、存储过程以及高级映射。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以使用简单的XML或注解来配置和映射原生信息，将接口和 Java 的POJOs(Plain Ordinary Java Object,普通的Java对象)映射成数据库中的记录。

###### 4-- Struts：

​	采用[`Servlet`](#ServLet)/[`JSP`](#JSP)技术，实现了基于Java EE Web应用的MVC设计模式的应用Web框架，是MVC经典设计模式中的一个经典产品。

​	通过应用Struts的框架，用户可以把大部分的关注点放在自己的业务逻辑(Action)与映射关系的配置文件(struts-config.xml)中。

​	主要控制负责MVC的分离，控制业务跳转，利用Hibernate框架对持久层(Dao)提供支持

###### 5-- Tomcat

​	Tomcat 由 Apache开发的一个`Servlet`容器，可以通过编辑XML格式的配置文件来进行配置。运行机理是Apache 为HTML页面服务，而Tomcat 实际上运行JSP页面和Servlet。

###### 6-- Maven

​	Maven是一个项目管理工具，且有较高的可重用性，所以常常用两三行 Maven 构建脚本就可以构建简单的项目。
​	Maven主要功能是：项目构建、项目依赖管理、软件项目持续集成、版本管理、项目的站点描述信息管理。

###### 7-- Ajax

​	异步JavaScript和XML， 使用Ajax技术网页应用能够快速地将增量更新呈现在用户界面上，而不需要重载（刷新）整个页面，这使得程序能够更快地回应用户的操作。

​	HttpAjaxRequest

## 3. 框架理解

#### Spring 开源框架

Spring框架是一个开放源代码的J2EE应用程序框架，是针对bean的生命周期进行管理的轻量级容器。

**特色**：

容器概念：Spring包含并管理应用对象的配置和生命周期

控制反转(IOC)：通过使一个对象依赖的其它对象会通过被动的方式传递进来以及工厂模式自动组装(只需要修改定义和参数配置)，实现低耦合。

面向切面(AOP)：允许通过分离应用的业务逻辑与系统级服务（例如审计和事务管理）进行内聚性的开发。



#### SSH与SSM

(Controller-Service-Dao)

由Struts2(使用Filter嵌入)+Spring+Hibernate构成

由SpringMVC(使用Servlet嵌入)+Spring+MyBatis构成

###### 1-- 两者的共同与不同点

- 相同点
  - 框架分为表示层、业务逻辑层、数据持久层、服务层和域模块层。
  - 都是以MVC为设计模式的开源框架

- 不同点
  - SSH注重配置开发，SSM注重轻量级配置。
  - Struts2 和 SpringMVC 中View和Model的交互机制不同，相较起来，SpringMVC更容易实现Restful风格。
  - Hibernate 和 MyBatis ORM框架使用环境不同
    - Mybatis有更为细致的SQL优化，自己写Sql语句。**但**需要维护SQL和结果映射(mapper)，数据库移植性不好，不同的数据库需要写不同的SQL。
    - Hibernate 对象的维护和缓存要更好,对增删改查的对象的维护要方便，自动生成Sql语句。**但**应对数据库变化能力较弱，SQL语句优化困难。

SSM目前为主流框架思想

###### 2-- SSM所谓的层

​	实体层(模块层)、持久层、业务层、表现层(控制层)、视图层

​	实体层：存放所需要的实体类，包括相关变量的JavaBean

​	持久层：一般是放置数据库操作的方法语句，负责与数据库进行交互设计。方法基本是接口，相关语句写在mapper.xml中

​	业务层：一般需要设计接口和接口方法，需要导入持久层

​	表现层：通过接收前端传过来的参数进行业务操作，需导入业务层

​	视图层：负责前台jsp页面的展示，需要Controller

#### SpringBoot

​	Spring Boot是基于Spring4的条件注册的一套快速开发整合包，实现了自动配置，降低了项目搭建的复杂度。

​	**特性**：1）去除xml配置        2）采用注解化配置         3）内嵌Tomcat



#### SpringCloud

## 4. JavaScript 和相关工具

#### 基本概念：

​	JavaScript是一种属于网络的高级脚本语言,已经被广泛用于Web应用开发，常用来为网页添加各式各样的动态功能,为用户提供更流畅美观的浏览效果。通常JavaScript脚本是通过嵌入在HTML中来实现自身的功能的。

#### 相关工具：



###### 

​	

​	

## 5. Jquery

[推荐网页](https://jquery.cuishifeng.cn/)

### 基本概念：

Jquery封装JavaScript常用的功能代码，提供一种简便的 JS 设计模式，优化HTML文档操作、事件处理、动画设计和Ajax交互。Jquery封装JavaScript常用的功能代码，提供一种简便的 JS 设计模式，优化HTML文档操作、事件处理、动画设计和Ajax交互。

### 选择器：

${selector}.action() ：相当于CSS中的选择器 document.getElementByxx

### 事件：

- 设置值         .text()
- 获得值         .html()
- Css样式      .css()
- 元素隐藏和消失  .show() / .hidden()

## 6. JSON

### 基本概念：

​	是一种轻量级的数据交换格式，简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

#### JSON与Xml的区别与优势：





## 其他知识

#### 接口

​	接口并不是类，编写接口的方式和类很相似，但是它们属于不同的概念。类描述对象的属性和方法。接口则包含类要实现的方法。



## 问题与解释

EJB、JB、POJO