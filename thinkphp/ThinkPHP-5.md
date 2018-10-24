ThinkPHP（5）
==========================

一、综合案例-完善部门管理
=========================

1、实现部门的删除功能
---------------------

控制器：DeptController.class.php

方法：del

**说明：删除有单个删除，也有批量删除；所以需要给列表页添加每一行的复选框**。

**第一步：先在列表上给每一行添加一个复选框**

![](media/2b7bb362e61d102a363928e6db2d84c5.png)

**第二步：要求点击【删除】按钮就可以实现删除**

![](media/285648a38defe94bf9ea20dc9c92476b.png)

点击删除获取到当前页面复选框中的值（jQuery实现），然后带着值跳转到删除方法del进行删除：

![](media/dbca1d9816c663954b57fbddacd1f3cd.png)

**第三步：编写del方法，实现删除**

![](media/c9b836206a4b010b2248f370117b5606.png)

二、综合案例-实现职员管理
=========================

1、准备工作
-----------

### 1.1、创建左侧菜单

将导航信息管理菜单设置成职员管理菜单：

![](media/3e568314c63c74c1d2f1cdcdcba3f276.png)

### 1.2、创建控制器

控制器名：User

![](media/56d01dbdf0e764772cd6f4cf33f947b4.png)

### 1.3、重新准备数据表

将db_oa中的数据清除，重新导入数据：

![](media/799699e8f4fbf9b5d837371b2cf6feec.png)

之所以是这样做，原因是之前对部门表进行了删除，导致职员表中的部门id在部门表中不存在。

2、实现职员添加功能
-------------------

控制器：UserController.class.php【已存在】

方法：add

模版：add.html

**第一步：创建add方法，负责展示模版**

![](media/a91de4bd58b1a48ed206b17a66fbbb0a.png)

**第二步：将模版文件add.html复制到指定的位置**

位置：./Application/Admin/View/User/add.html

![](media/ae4c0dd1e0120274facbcdc32d969a79.png)

**第三步：改写add方法，查询出部门的信息，然后展示在模版中下拉列表上**

![](media/b914c1872168b0e0d02a98c72dd0b5c0.png)

**第四步：需要将data变量在模版中展示**

![](media/cb371c832d9f3e4297b267537da9d802.png)

**第五步：检查模版**

修改action值，提交到当前页面可以不写action的值，也可以写成当前控制器下的add方法

![](media/54e600c3378439b415191aa692214534.png)

通过jQuery提交表单：

![](media/7c36c435e4cc94f25fe6d08f0843845e.png)

jQuery已经在模版中写好了。

表单中使用了时间控件：

![](media/5202b993a1ae07e352187ee28a337bf3.png)

![](media/e5cc3cd6f3fb4e3a7272097917526ccd.png)

时间控件必须放在jQuery之后。

**第六步：改写add方法，编写处理表单提交代码**

![](media/446f8ff463c34a9b1bcc41041728f90b.png)

在数据表中的体现：

![](media/aa3d8cdaca8676b68a506ed9218419e5.png)

3、实现职员列表功能
-------------------

控制器：UserController.lcass.php

方法：showList

模版：showList.html

**第一步：创建showList方法，展示数据和模版**

![](media/de5a2336fd7f0eeb80395babaacf2a38.png)

**第二步：将模版文件showList.html复制到指定的位置**

位置：./Application/Admin/View/User/showList.html

![](media/75661ad6b4403a60bf74e119fa1d2f90.png)

**第三步：将data数据在模版中展示**

分析：由于data是select的返回结果所以是二维数组，在展示的时候需要进行遍历操作。

![](media/d9b265e24478eab1cf7b540754d096cb.png)

显示结果：

![](media/6b6c3edfc0b9c81d1806f7dd96a43375.png)

三、ThinkPHP中的功能类-数据分页类
=================================

数据分页它是通过limit语法来实现。分页类的核心就是limit语法。

在ThinkPHP中系统封装好了一个分页类：**Page.class.php**

1、介绍
-------

属性：

![](media/9014fad7e590ef6c65d612a4e5fcf570.png)

方法：

构造方法：

有三个参数，但是至少得传递第一个参数（总的记录数），一般还要指定第二个参数（每页显示的记录数，如果不指定则默认显示20个）

![](media/22c5df02b25ea5eae3a495b0579e9aac.png)

SetConfig方法：通过public类型的setConfig方法来设置私有属性config

![](media/1bd1e10a07c3f5c7680d1a28ea526059.png)

Show方法：生成页码及页面页码上的URL连接

![](media/6774c51a4cb4d805abdeb1960db37810.png)

**制作分页效果的步骤（七个步骤）：**

![](media/062440b032334e89c6a44595accb1322.png)

**第一步：查询出总的记录数；**

**第二步：实例化分页类，由于底层实现要求实例化的时候至少需要传递总数，所以需要在实例化的时候传递参数；**

**第三步：（可选步骤）定制显示分页提示的文字；**

**第四步：通过show方法输出分页页码的连接；**

**第五步：使用limit方法进行分页查询，注意其参数是page类的属性；**

**第六步：使用assign将查询的数据和分页连接数据传递给模版；**

**第七步：输出模版；**

2、使用数据分页类实现职员管理的分页功能
---------------------------------------

**第一步：查询总的记录数**

![](media/53f3d7d1eb9680ff546f0ee18975dbb7.png)

**第二步：实例化分页类，传递参数**

![](media/2bd087f4066c5491c784471d6dab99e2.png)

**第三步：（可选步骤）定制分页按钮的提示文字**

**设置首页和末页的时候需要注意，如果总的页码数小于分页类中rollPage属性，则不会显示首页和末页的按钮，这个时候需要修改rollPage的值；由于分页类中lastSuffix属性，定义最后一页显示总页数，所以将其改为false**：

![](media/4e198b0bbb5d810da42a5eb118321192.png)

**第四步：通过show方法输出分页的URL链接**

![](media/66161d69a3e1b49c8cef0b5c240cb8bb.png)

Show方法返回值类似于下面的这种形式：

![](media/6cc1f11e5faaebccf5347cbbba5e896b.png)

**第五步：使用limit方法查询数据**

![](media/dee6e7e3ac3caf5870d4cd99f6e8f5c5.png)

**第六步：传递数据**

![](media/9e830310691b8b3b360b621f89755f74.png)

**第七步：展示模版**

![](media/9724c8559251aa7dba74f36646a1f904.png)

在模版中展示show变量：

![](media/183fb3a223b65a5b066c358d8be2a9ac.png)

说明：在以后的实际开发过程中，分页的样式由前端人员编写。

显示效果：

![](media/15231542b7b4482cde82fe1fc0501dd0.png)

<br>四、联表查询（重点）
========================

在原生的sql中使用join语法来进行数据表的联表查询。

在ThinkPHP中，系统也是支持联表查询操作，但是可以归纳成两种方式：table方法、join方法。

1、table方法
------------

原生的语法中table方法的语法：**select 表1.字段,表2.字段 from 表1 as 别名1,表名2
as 别名2 where 表1.字段 = 表2.字段**;

Where的语句含义：也就是通过where语法来进行两个表的关联操作。

案例：查询每个职员的全部信息，要求使用table语法。

分析：因为职员信息中，有一个字段“dept_id”，这个字段是部门表中的主键，所以此处应该读取出部门的名称。所以要求关联部门表。**关联的条件是职员表中的dept_id等于部门表中的id**。

**主表：sp_user 别名：t1**

**从表：sp_dept 别名：t2**

原生的sql语句：**select t1.\*,t2.name as deptname from sp_user as t1,sp_dept as
t2 where t1.dept_id = t2.id;**

在navicat中执行的结果：

![](media/51642e4cae5599704700169816eaf9e4.png)

将上述的代码，在ThinkPHP中实现查询的效果：

**方法1：可以使用执行原生的sql语句进行执行**

![](media/3a9d96362429102ea5252b9f286f9b07.png)

**方法2：可以使用table方法实现**

在ThinkPHP中一般不建议频繁的使用执行原生的sql语句方法执行sql，所以上述的方法还可以写成另外的一种形式：

**\$model -\> table(‘表名1 [as 别名1],表名2 [as 别名2]…’);**
//table方法也是连贯操作中的一个辅助方法。**在使用table方法之后模型会自动关联上table方法中指定的数据表**。

下面可以使用table方法改写之前的原生的sql：

![](media/803b9dfbd67b6f35f469fe6b82533be8.png)

执行结果中的sql：

![](media/3e65c42d4019e182d0b84a5d57517835.png)

2、join方法
-----------

![](media/35861824c941f3f92e239683b077ca4d.png)

在join语法中，上述圈出的用的比较多。

在原生的sql中，join的语法：**select 表1.字段,表2.字段 from 表1 as 别名
[inner/left/right/full] join 表2 as 别名 on 表1.字段 = 表2.字段;**

案例：查询部门的详细信息，列出每一条部门信息中的pid对应的部门名称。

**说明：在以后的实际使用的时候，会遇到一种关联情况就是自己关联自己，自联查询**。

**主表：sp_dept 别名：t1**

**从表：sp_dept 别名：t2**

**条件：t1.pid = t2.id**

原生的sql：**select t1.\*,t2.name as deptname from sp_dept as t1 left join
sp_dept as t2 on t1.pid = t2.id;**

将上述的sql放到navicat中执行：

![](media/ad189048cb4fca34c833634e416a97eb.png)

在ThinkPHP中去执行上述的代码：

Join联表语法：

**\$model -\> join(‘联表方式 join 表名 [as 别名] on 表1.字段 = 表2.字段’);
//join方法也是连贯操作的辅助方法之一，只有一个参数**。

如果需要给当前模型关联的表起别名的话，则可以使用alias方法：

\$model -\> alias(‘别名’); //alias也是辅助方法之一

![](media/2758b248ae25199464de8cb3510eb2e5.png)

执行结果：

![](media/f568bf9e7448ba0a8bfa591ef0101737.png)

跟踪信息中的sql：

![](media/5e65b60aa3b94f31d3fd338bfb075d7b.png)

<br>五、highcharts
==================

1、介绍
-------

一款基于jQuery开发的图表插件。国外插件，在国内也有一款类似的echarts（百度开发的）。

官网：<http://www.highcharts.com/>

下载地址：<http://www.highcharts.com/products/highcharts>

Demo网址：<http://www.highcharts.com/demo>

下载之后会得到一个压缩包：

![](media/c31f3ec876d503a3a3585f1a1180c4ac.png)

![](media/b0adbacdc01e7374899939030cbb65d1.png)

2、综合案例-使用highcharts实现部门人数的统计
--------------------------------------------

案例要求：就是使用图表形式统计出每个部门有多少人。

**第一步：先从examples目录中找到适合当前案例的demo代码。**

确定使用目录为column-rotated-labels中的代码

![](media/f50ffe9a13d96920d41483066b4cca73.png)

**第二步：分析demo**

分析使用步骤：

**第一步：引入jQuery文件；**

**第二步：替换data数据；**

**第三步：引入highcharts.js和modules目录下的exporting.js；**

**第四步：声明一个div，放置图表（图表容器）；**

**第三步：修改模版文件User/showList.html**

将下面的统计按钮设置链接，点击之后跳转到统计表页面：

![](media/bac52a8e4dad690f4678430f69092072.png)

![](media/89bcd94847f2250a99a81144c832fe94.png)

定义图表页面的方法：charts，写在user控制器中，展示图表的模版文件：

![](media/4e8009943ea705010f40943905b13a39.png)

**第四步：将demo文件复制到模版的位置，同时还需复制静态资源文件**

![](media/5a34fd0580ecd7c73bf1fa525f1b78ea.png)

将highcharts整个解压目录复制到/Public/Admin/plugin（后期所使用的插件都会放到这个目录中）：

![](media/0da4eaa1bff8810de4a87cb8b984f8cd.png)

将模版中对应的静态资源文件的路径做修改：

引入jQuery：

![](media/4aa8d3f7f551fe2fa253f3601c08fba1.png)

引入highcharts.js文件和exporting.js文件：

![](media/b2e3f79bd346964c6b2a1e8e6d730080.png)

**第五步：改写charts方法查询出数据，替换掉demo中原先的数据**

统计部门有多少人，最终的形式应该是类似于：

**产品部：10,**

**管理部：5,**

**技术部：20**

**…**

需要联表查询（sp_user，sp_dept）：

**主表：sp_user t1**

**从表：sp_dept t2**

**关联条件：t1.dept_id = t2.id**

原生的sql写法：**select t2.name as deptname,count(\*) as count from sp_user as
t1,sp_dept as t2 where t1.dept_id = t2.id group by deptname;**

在navicat中执行结果：

![](media/f58e153fd2023df7706f2c44516ff7ca.png)

连贯操作写法：

![](media/bb830ca356110a96afaf4740f210349a.png)

数据str已经传递到模版中，替换掉原先的数据：

![](media/3ac05c686886592fd9be2b047c2ced33.png)

**第五步：细节完善**

修改表头：

![](media/663e6b882a6f9cceef300e2bbe3722f3.png)

修改左侧的单位信息：

![](media/e4359fd8a9353a6400bbde9c8366a103.png)

鼠标悬浮效果：

![](media/caf70013ec018e868393bf5ff561e1e2.png)

图表上的小数点的处理：

![](media/5054ffef5305519995eae88ab8268f41.png)

最终显示效果：

![](media/3222189f0f44f00f7c40159e6d307c1f.png)

六、作业
========

-   实现职员管理中的职员编辑和删除

-   独立完成今天所讲的案例
