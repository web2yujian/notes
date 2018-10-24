# AngularJS学习笔记

## 一、AnjularJS简介

- 关于AngularJS的特点：

  1）**数据的双向绑定**，这可能是其最激动人心的特性，view层的数据和model层的数据是双向绑定的，其中之一发生更改，另一方会随之变化，而不需要写任何代码；

  2）**代码模块化**，每个模块的代码独立且拥有自己的作用域，比如model，controller等；

  3）**强大的directive**，可以将很多功能封装成HTML的tag，属性或者注释等，这大大美化了HTML的结构，增强了可阅读性；

  4）**依赖注入**，将这种后端语言的设计模式赋予前端代码，这意味着前端的代码可以提高重用性和灵活性，未来的模式可能将大量操作放在客户端，服务端只提供数据来源和其它客户端无法完成的操作；

  5）**测试驱动开发**，使用Angular开发的应用可以很容易地进行单元测试和端对端测试，这解决了传统的JS代码难以测试和维护的缺陷。

- AngluarJs第一次编程

  ```html
  <!DOCTYPE html>
  <html ng-app="">
  
  <head>
      <title>hello world</title>
  <script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>
  </head>
  <body>
  <!--code-->
    Hello {{'World'}}!
  </body>
  
  </html>
  ```

- AngularJS应用场景

  > - AngularJS主要考虑的是构建CRUD（增加Create、查询Retrieve、更新Update、删除Delete）应用。幸运的是，至少90%的WEB应用都是CRUD应用。 如果你要开发的是**单页应用**，AngularJS就是你的上上之选。
  >
  > - 但是像游戏开发之类**对DOM进行大量操作**、又或者单纯需要**极高运行速度**的应用，就不适合使用AngularJS了。

- 

## 二、AngularJS中的指令

### 1. ng-app

### 2. ng-bind

### 3. ng-repeat

### 4. ng-





