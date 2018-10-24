PHP高手之路之ThinkPHP（7）
==========================

一、综合案例-完善公文管理
=========================

1、实现公文的编辑
-----------------

控制器：DocController.class.php【已存在】

方法：edit（将展示模版和数据的保存写在一起）

模版：edit.html

**第一步：修改模版文件showList.html，在每行后面添加一个【编辑】按钮，点击之后跳转到编辑页面（edit方法）**

![](media/3404e76529248c1d6dc8df99b3f8fd5c.png)

显示效果：

![](media/590a05e34a4fd24a3964a012429ad579.png)

**第二步：在控制器中编写方法edit，展示数据和模版**

![](media/0802898ce7fb4211a1e5d0ba9062edde.png)

**第三步：将模版文件edit.html放到指定的位置**

位置：./Application/Admin/View/Doc/edit.html

说明：此处的模版文件可以直接复制add.html来使用，并且改名为edit.html

![](media/45cd3465cc52fff2989cd8cb6a5f5482.png)

**第四步：在edit.html模版中展示当前修改记录的原始数据**

![](media/966b235e0bd8856d07a743b3bfdbf785.png)

说明：

**1、关于文件域的值：在文件域中输出value属性没有意义，所以我们可以采用和修改密码一样的原理，如果用户选择了文件，则表示修改，如果没有选择，则表示不修改文件；**

**2、由于content字段，在之前写入数据表的时候接收通过I方法进行了转码处理，所以在展示的时候还需要解码，还原之前的形式，需要使用到htmlspecialchars_decode。**

**第五步：检查表单**

![](media/6e5db42ee7dc29889cf17c493d948068.png)

**在表单中添加一个隐藏域（通过隐藏的表单项来传递一个值），值可以是\$data.id，也可以写成{\$Think.get.id}。**

**第六步：改写edit方法，判断请求类型，实现数据的保存**

![](media/de77be187ad6cf8b24828bb79a31f836.png)

实现数据的保存提交：

![](media/6486beff2df3549a6032e63a0edaacde.png)

模型中的自定义保存数据方法updateData：

![](media/aed39507a3c79483e26a5b74ebec23af.png)

二、综合案例-实现知识管理
=========================

1、准备工作
-----------

### 1.1、数据表

数据表名：sp_knowledge

![](media/0fd4f5abb391beae77cf7c8cc9cb6dd1.png)

创建结果：

![](media/fb9d3af827e93b5eb6b290847a6d59c3.png)

### 1.2、导航菜单

修改模版文件Index/index.html文件，创建导航菜单：

![](media/67e6c053f604ec673c8ab65e8e206f70.png)

![](media/55bf6a2309edb0baca492f43d55884cc.png)

### 1.3、创建控制器

**控制器文件名：KnowledgeController.class.php**

![](media/ce284eb031b2987a10ccd11673109fba.png)

2、实现知识的添加功能
---------------------

控制器：KnowledgeController.class.php【已存在】

方法：add（二合一）

模版：add.html

**第一步：创建方法add，展示模版文件add.html**

![](media/dc8899861cc1990089098ab97859af34.png)

**第二步：将模版文件add.html复制到指定的位置**

位置：./Application/Admin/View/Knowledge/add.html

![](media/7615fe59f5365ad5112f4b5d0d3d03a2.png)

**第三步：检查表单**

注意：

1、如果有文件上传则需要有enctype属性；

2、要求文件域是file类型；

3、请求类型是post；

![](media/bf3e3fb341e710fe8d7390d808751e3b.png)

![](media/3d52b46a3d85ba6a0473e3d57a328093.png)

**第四步：改写add方法，处理表单的提交数据的保存**

![](media/be5acab85b3eb3d56e0d42ab0a3b8dfd.png)

**第五步：编写自定义模型的代码**

创建自定义模型：KnowledgeModel.class.php

![](media/1f404239994a3f7db4de32ccfdcbc638.png)

实现代码，编写方法：

Public function addData();

缩略图的制作：

需要使用到功能类：Image.class.php（图像处理类）。

**注意：如果使用图形处理类，则必须开启GD2扩展库**。

方法：

构造方法：__construct

![](media/c4109e801a8f0fb80b112a2d814787c7.png)

其中形参都是可选的，所以在实例化的时候可以不传递任何的参数。

Open方法：打开图片，一般情况下，参数是图片的路径（建议使用绝对路径）

![](media/8557c4966af598d463377bc92669084e.png)

Thumb方法：参数一般只传递前2个即可（宽高）**等比缩放的原则。举个栗子，如果之前的图片宽高是2000:1000，即使我们设置缩略图的比例是100:100，则生成的结果还是100:50**。

![](media/929ef0fcfafbeb1977d2f69f28794ec9.png)

Save方法：保存图片，只需要传递第一个参数图片保存完整路径即可

![](media/4a16b30520cf1158e3638ab7a07eab82.png)

根据上述的方法，如果不考虑实例化图形类则我们可以归纳出制作缩略图的步骤大致为：

**第一步：打开图片；**

**第二步：制作缩略图；**

**第三步：保存图片；**

具体可以参考手册中的demo代码：

![](media/83ee87b1713ea3919411d8abd351cf74.png)

特别说明：**因为在图形处理类中所有的执行方法返回值都是\$this说明2点，第一个点就是可以使用连贯操作的形式，第二个点就是没有办法判断图形处理是否成功**。

保存测试数据：

![](media/5f5c1bb725ddfdf9784a42b798c84d36.png)

实现上传代码：

![](media/8fa1682b18f7f9b58592990fe6a086db.png)

制作缩略图：

![](media/5beee9e36734cec0536cb52638f72303.png)

数据表中的数据：

![](media/ed23ab685933474c98fec3cd79664b33.png)

3、实现知识的列表功能
---------------------

控制器：KnowledgeController.class.php

方法：showList

模版：showList.html

**第一步：创建方法showList，获取数据，展示数据和模版**

![](media/b2fa91261b6ac15c2352c6a6977583f3.png)

**第二步：将模版文件showList.html复制到指定的位置**

位置：./Application/Admin/View/Knowledge/showList.html

![](media/ea957ba0b11e51bd565b335bd2aafd31.png)

**第三步：在模版中遍历数据data，在模版中展示**

![](media/d0cdc09d4c61717424fa1d8812485fb7.png)

显示效果：

![](media/e8d59dcacb3a1ab41a424e7ae3d6ba3e.png)

**第四步：实现图片的下载**

可以通过empty标签来判断是否有图片：

![](media/76aff2cec5f32b35baad7c2f544ca16a.png)

显示效果：

![](media/404db6cd1566ed18c073c7bf84bcd4e8.png)

编写download方法实现下载：

![](media/93ef168b853f2ef6bd25d3954f965116.png)

三、综合案例-实现邮件管理
=========================

邮件：这里指的邮件不是一般所说的email邮件（邮件地址带有\@符号的），指的是一般论坛网站的站内消息（私信，pm---private
message）。站内信一共可以分为以下几个组成部分：**邮件发送、邮件收件箱、邮件发件箱**。

1、准备工作
-----------

### 1.1、数据表

数据表：sp_email

![](media/935a44c46e7ff74d9f851403241d823b.png)

创建成功：

![](media/5608550b3048976c19d2eaf2221403e3.png)

### 1.2、导航菜单

修改文件Index/index.html，将邮件管理的菜单显示出来：

![](media/dd16a5cb053d73d174233280389015ca.png)

### 1.3、创建控制器

**控制器文件名：EmailController.class.php**

![](media/81b3f7195be7c9986ab83142b16cfa87.png)

2、实现邮件的发送功能
---------------------

控制器：EmailController.class.php【已存在】

方法：send（二合一，展示模版+数据保存）

模版：send.html

**第一步：创建send方法，先展示邮件发送功能的模版页面**

![](media/a522e6bb72e801f3591a109d29e94b56.png)

**第二步：将模版文件send.html复制到指定的位置**

位置：./Application/Admin/View/Email/send.html

![](media/4d430c8e92d5b08dca121d172f29b8a2.png)

在模版中要求选择收件人，所以需要去改写send方法去展示收件人获取收件人的信息：

![](media/1ea076ac09de973bcc27a0c5d8563c08.png)

**第三步：改写send方法，查询收件人的信息，展示在模版中**

![](media/431a549ca6a4f84473f710783d148b0e.png)

**第四步：在模版中展示收件人列表**

![](media/f459343b2ce7f34a4c30e64d79de4416.png)

**第五步：检查表单**

Form标签：

![](media/f03723da2418c979384f87919f0e982a.png)

文件域：

![](media/6d84626023f4a3a509b61c383c4af1ac.png)

**第六步：将数据在提交之后保存到数据表中**

先判断请求类型，如果是post请求，则处理数据；如果是其他则展示数据和模版：

![](media/8801b62262a4f3703529b6f0659d8cab.png)

创建自定义模型：

![](media/863a6deab74288c511fcbd8fc19a5b10.png)

编写需要的addData方法实现数据处理和保存入库（文件处理+数据处理）：

![](media/6e4b27c3e2ee4e62d88e3535b6ba039e.png)

此时，功能代码已经全部的编写结束，测试邮件发送功能，在数据表中发送结果如下：

![](media/489162fcf0714d67543d996d1c72449e.png)

如果数据表中有刚才提交的数据，则表示邮件发送成功。

3、实现邮件的发件箱功能
-----------------------

控制器：EmailController.class.php

方法：sendBox

模版：sendBox.html

**第一步：创建方法sendBox，获取列表数据，展示数据和模版**

**注意：当前功能是发件箱，在发件箱中需要显示出收件人的名字。（此时数据表中存储的是收件人id，to_id因此，需要联表查询数据）。**

**主表：sp_email t1**

**从表：sp_user t2**

**关联条件：t1.to_id = t2.id**

原生的sql语句：**select t1.\*,t2.truename as truename from sp_email as t1 left
join sp_user as t2 on t1.to_id = t2.id where t1.from_id = 当前用户的id;**

将上述的sql代码复制到navicat中去执行：

![](media/6a466994f069180cde9febba2e0ffca3.png)

将上述代码在ThinkPHP中去执行：

![](media/830f29ea8ab7b0a55321c4d258feca4a.png)

**第二步：在模版中展示数据**

将模版文件sendBox.html复制到指定的位置

位置：./Application/Admin/View/Email/sendBox.html

![](media/42230867c9a5da2f1bf0e5b807d94a25.png)

![](media/a80917aaab4bb8895dfd3caa42befb97.png)

显示效果：

![](media/edbd0d4de31c1b5fdf7ddaaf1c7f88bb.png)

**第三步：实现附件的下载**

如果有附件，则显示附件的下载，没有则不显示下载按钮

![](media/4a4e937e4e14bbf8beb2346823bcda7d.png)

显示效果：

![](media/aa66b26ec134097a02fc68978d254c37.png)

在控制器中编写download方法：

![](media/10e1cff09685e3518ddf03da611dbf3b.png)

四、扩展（3）
=============

1、空操作
---------

空操作是指系统在找不到指定的操作方法的时候，会定位到空操作方法来执行（针对控制器也是如此），利用这个机制，我们可以**实现错误页面**和一些URL的优化。

**关于空操作的说明：**

**1、空操作方法：在控制器中可以定义一个操作方法名字叫做_empty()；**

**2、空操作控制器：在ThinkPHP中存在一个空的控制器，当指定的控制器找不到，则会去访问空的控制器，空控制器的文件名叫做EmptyController.class.php。**

空操作方法实现：

例如，下面的空操作方法，我们写在Email控制器中，则如果访问email控制器中的方法不存在，则会默认访问_empty方法。

![](media/dc2401a2c5796fa0bb0f3ce8801da1fa.png)

空的控制器实现：

创建空的控制器：EmptyController.class.php

![](media/89dc933f65b22fe65276e9b495fd31b9.png)

上述的代码会在访问的控制器不存在的时候进行调用。

案例：使用空操作方法实现404页面的自定义。

模版文件：

![](media/31f9d2d5159dc6abf0872d80aed1812e.png)

**第一步：将模版文件复制到指定的位置**

![](media/ec47c5ae4a12ef690aae58111e2634d5.png)

同时将静态文件放到指定的目录中：

![](media/6cb9de7b0388db0c6dfb2c1200b04650.png)

修改模版中的原图片引入路径：

![](media/c66a314b7cd08154de55e144714986ef.png)

**第二步：在空操作控制器中的空操作方法展示错误的模版页面**

![](media/72d2c8f69d249ee7b6e8c19f7bfb3f01.png)

显示效果：

当控制器存在，方法不存在的时候：

![](media/b25df8e824e10c13348f9a171749c586.png)

当控制器不存在的时候：

![](media/1b3b695e85cfd87eeea936063c710032.png)

<br>五、jQuery中的ajax回顾
==========================

在jQuery中ajax方法一共有几个？

有4个：**get、post、ajax**、getJson（解决跨域的时候使用）

1、\$.get方法
-------------

-   jQuery.get(url,[callback],[type])或者 \$.get(url,[callback], [type])

在jQuery中\$表示jQuery。

![](media/15c8205d1eaa894c8de3ffcaaa6bfba2.png)

参数说明：

url：必须的参数，表示请求的url地址；

callback：可选参数，表示请求成功之后触发的回调函数；

type：可选参数，期望的返回数据类型，常见的类型有：**json**、xml、text、html；

2、\$.post方法
--------------

-   jQuery.post(url,[data],[callback], [type])
    或者\$.post(url,[data],[callback], [type])

参数：

url：必须，请求地址；

data：可选，给url传递的post参数；

callback：可选，执行成功之后的回调函数；

type：可选，期望的返回数据类型；

3、\$.ajax方法
--------------

Ajax方法是jQuery中ajax方法（get和post）的底层实现方法：

语法：

\$.ajax(json对象)，参数只有一个，那就是json对象

Json对象中的属性：

•async 是否是异步，默认是；

•cache 是否使用缓存，默认是，当dataType为jsonp或者script的时候默认是否

•complete 当请求执行完成的时候触发的回调函数，完成不一定表示成功。

•data 表示传递的参数，是一个json格式

•dataType 期望的返回数据类型，有json、xml、text、html等等

•success 表示请求成功之后触发的回调函数

•type 表示请求的类型，如get、post

•url 请求的地址
