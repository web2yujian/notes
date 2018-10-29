## 一、Smarty模板引擎

**1.Smarty模板引擎简介**





![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181029084518.png)

> Smarty分离了逻辑代码和外在的内容，提供了一种易于管理和使用的方法，将原本与HTML代码混杂在一起PHP代码逻辑分离。简单的讲，就是要使PHP程序员同前端人员分离，程序员改变程序的逻辑内容不会影响到前端人员的页面设计，前端人员重新修改页面不会影响到程序的程序逻辑，这在多人合作的项目中显的尤为重要。

- **Smarty模板引擎优点：**

    1）速度：相对于其他模板技术而言，采用Smarty编写程序可以获得最大速度的提高。

    2）编译型：采用Smarty编写的程序在运行时要编译成一个非模板技术的PHP文件，这个文件采用了PHP与HTML混合的方式，在下一次访问模板时将WEB请求直接转换到这个文件中，而不必进行重新编译模板（在源程序没有改动的情况下）

    3）缓存技术：Smarty选用的一种缓存技术，它可以将用户最终看到的HTML文件缓存成一个静态的HTML页，当设定Smarty的cache属性为true时，在Smarty设定的cachetime期内将用户的WEB请求直接转换到这个静态的HTML文件中来，这相当于调用一个静态的HTML文件。

    4）插件技术：Smarty可以自定义插件。插件实际就是一些自定义的函数。

    5）模板中可以使用if/elseif/else/endif。在模板文件使用判断语句可以非常方便的对模板进行格式重排。

- **不适合使用Smarty的地方：**

    1）需要实时更新的内容。例如像股票显示，它需要经常对数据进行更新，这类型的程序使用smarty会使模板处理速度变慢。

    2）小项目。因小项目简单而使美工与程序员兼于一人，使用Smarty会在一定程度上丧失PHP开发迅速的优点。

#### **2.Smarty模板引擎原理**

> **Smarty模板引擎的原理：**把模板文件编译成php文件，然后每次都去读取模板的修改时间，没有修改就不编译。然后include这个“编译”后的PHP文件。所谓编译也就是模板用正则替换成含PHP代码的过程。模板文件和php程序文件经过模板引擎的编译后合成一个文件，即编译后的文件。



![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181029084929.png)

#### **3.Smarty开发模式与运行流程**



>  Smarty的这种开发模式是**基于MVC框架概念**。MVC全名是Model View Controller，是模型(model)－视图(view)－控制器(controller)的缩写。MVC已经成为一种软件设计典范，它用一种业务逻辑、数据、界面显示分离的方法组织代码，将业务逻辑聚集到一个部件里面，在改进和个性化定制界面及用户交互的同时，不需要重新编写业务逻辑。



- **Model**（模型）是应用程序中用于处理应用程序数据逻辑的部分。

通常模型对象负责在数据库中存取数据。

- **View**（视图）是应用程序中处理数据显示的部分。

通常视图是依据模型数据创建的。

- **Controller**（控制器）是应用程序中处理用户交互的部分。

通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。

Smarty模板引擎将PHP程序直接生成模板文件，最终浏览器中读取的就是Smarty模板文件，并且Smarty能够对模板文件进行判断，如果是第一次或者模板已经改变，则重新生成。

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181029085227.png)





## 二、学习Smarty模板

#### 1.下载解压

- 根目录：

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181029091320.png)

#### 2.结构介绍

- libs下：

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181029144725.png)



- demo下：

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181029151603.png)

