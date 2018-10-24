PHP高手之路之ThinkPHP（6）
==========================

一、综合案例-实现公文管理的相关功能
===================================

1、准备工作
-----------

### 1.1、创建数据表

表名：sp_doc

![](media/47f40b81a4965974faef92a9224fe4b0.png)

创建成功：

![](media/11c3182dd75c96ea06749344607471ab.png)

### 1.2、创建控制器

控制器：DocController.class.php

![](media/7eb0be3af0124fe0d6b93543a59727e1.png)

结构代码：

![](media/c306be55f56fa4f99b948ed074437e88.png)

### 1.3、创建二级导航

修改模版文件Index/index.html，修改出公文管理的导航菜单：

![](media/13aff515df94d2cb3a401525648a5f29.png)

修改二级导航的链接，列表方法还是使用showList，添加方法还是使用add。

2、实现公文的添加功能
---------------------

控制器：DocController.class.php【已存在】

方法：add（**二合一，将模版展示和保存处理写在一起**）

模版：add.html

**第一步：在控制器中创建add方法，展示模版文件**

![](media/8dd9345bdc01c3f5a2afeea93e2750bf.png)

**第二步：将模版文件add.html复制到指定的位置**

位置：./Application/Admin/View/Doc/add.html

位置中的Doc是不存在的，需要自行创建。

![](media/df5fe5eca54deb7999de8e53db0d92ae.png)

**第三步：检查表单**

Action：由于是提交给当前页面处理的，所以action可以不写

Ectype：声明当前表单中存在多媒体文件，只要是用了附件上传，则必须需要这个属性

![](media/95d76eabcf33f5eb9b82104a810985b7.png)

文件上传域的type类型：

![](media/629b8c1768863c06fde9514102fc4265.png)

表单的提交，通过jQuery实现：

![](media/22a25f09a5d15c83b502488bfba8f2cb.png)

![](media/a8f60ea4de526e763ca63219e454978d.png)

**第四步：不考虑文件上传，将其他的几个字段的数据，先实现入表保存**

![](media/6405c70ed70819eee27533b1611e9379.png)

保存结果：

![](media/4dced854b155173da82440c799ca8336.png)

3、实现公文的列表功能
---------------------

控制器：DocController.class.php

方法：showList

模版：showList.html

**第一步：编写showList方法，查询数据，传递数据，展示模版**

![](media/61940e929f0bd7cbe50e2f41a0223176.png)

**第二步：将模版文件showList.html复制到指定的位置**

位置：./Application/Admin/View/Doc/showList.html

![](media/cdde90b6466eff82f4b8ea5e7b0a385f.png)

**第三步：将模版变量data，展示在模版中**

分析：由于data是select的返回结果，是一个二维数组，所以需要遍历操作进行展示

![](media/254f50d832c6510efaf2db0ec067be5e.png)

显示效果：

![](media/daf96b693fa7fc20325360d96e792bfe.png)

会发现，在标题一列，由于字数过多，导致多行显示的效果，影响美观，需要进行美化的处理：

![](media/85690b600f21d0ec34e8a559f8d0bb7a.png)

**我们可以参考百度新闻的显示效果，对于多的字符进行截取，然后后面显示省略号**。

目前在提供的函数库文件中已经封装好了一个msubstr的函数，该函数可以进行中文截取：

**将function.php放到指定的位置（建议放到应用级别的目录中/Application/Common/common）**

![](media/5244e0701861f0155eccf06c08a7539c.png)

![](media/1bd6e816d7c5954e3a7e25dd474bb0e0.png)

参数说明：

**\$str：需要截取的字符串**

**\$start：表示开始位置**

**\$length：表示截取的长度**

**\$charset：表示字符串的字符集**

**\$suffix：表示是添加省略号**

![](media/998ae50fa78f7129865ac7a09c57630e.png)

显示效果：

![](media/2cc122d85178a85a542cb356540856ca.png)

说明：msubstr函数在function.php中已经定义，所以只需要将function.php移动到指定位置之后就可以在模版中使用。

二、ueditor
===========

1、介绍
-------

Ueditor是一款在线编辑器插件，在线编辑器又称为“富文本编辑器”。作用是为了方便图文混排操作，国外也有一款类似的插件，叫做CKeditor。

UE是百度公司开发的在线编辑器，官网：<http://ueditor.baidu.com/website/>

![](media/a1cf80d177b93a395fee5b5cf8d3b142.png)

下载：

![](media/a5339929561f0725bea49c1a876eb568.png)

下载之后会得到一个zip格式的压缩包：

![](media/378bc72e450a7aecb42ee3b66611938b.png)

在压缩包中有一个index.html，它是demo文件：

![](media/fe95815f8409c2623b1cff293d5ca216.png)

通过demo文件中的代码，可以分析出，使用UE的步骤一共是有三步：

**第一步：引入外部的资源文件（javascript文件）。**

![](media/fce945ec485311b290d09adc1e29bd8e.png)

**Ueditor.config.js**

**Ueditor.all.min.js**

**Zh-cn.js**

**第二步：指定标签，设置容器的位置（编辑器显示的位置）。**

![](media/6f5f570f17fbc6289cedb3536283e684.png)

上述代码是通过id来指定容器的名字，后期实例化容器的时候需要指定的id。

**第三步：实例化容器，生成编辑器效果。**

![](media/ad619a44beb3788d6f54545c4ebc82dd.png)

2、使用UE编辑器替换掉公文管理中的原先效果
-----------------------------------------

**第一步：将utf8-php解压目录复制到公共静态资源文件目录下的插件目录（plugin），改名为ue**

![](media/4ab245810263f359bf16472f898fdf42.png)

**第二步：在目标模板文件add.html中引入三个需要的javascript文件**

![](media/16852178b84f1fd16e467291ab98cdb5.png)

**第三步：设置标签，定义富文本编辑器的位置**

将demo文件中的容器位置定义的代码复制替换掉textarea标签：

![](media/6ac25b213d8b167c3ab69068a1d11550.png)

**第四步：实例化容器**

复制demo中的实例化代码：

![](media/c4830e7dc0375c1602af5f62293669e2.png)

显示效果：

![](media/a9278800340bee878c7d77330fbdab61.png)

显示效果存在2个问题：

第一个问题：将【内容：】覆盖了

第二个问题：宽高有点大

进行适当的调整容器：

![](media/61cb17b890551efc2f88b0bf7b241a73.png)

调整后的结果：

![](media/7e821d3921361a6f52a76d693b17c7b3.png)

**第五步：测试ue的提交结果**

![](media/6e6ff10d14e35d24c4213bfbb449ed35.png)

通过上述的结果，我们可以发现2个问题：

**1、ue编辑器默认的name值是editorVlue，默认值和数据表中的字段名是不一样的，在后期添加的时候会被过滤，这个问题如何解决？**

解决办法：只需要给当前容器的标签指定一个name值就可以了。

![](media/cf3a78c377246d763b38b24f1c115835.png)

![](media/f787067b3ec72e30eb27bcab83814f58.png)

**2、在UE的源码中的一些样式会被转化成实体字符，是谁去转化的实体字符呢？**

答：此处的转码，是由ThinkPHP的I方法进行转化的，使用的是htmlspecialchars。

关于使用UE的几个说明：

**1、防止sql注入和xss：光通过I方法解决不了，在后面我们会使用一个插件htmlpurifiy来对指定的标签进行过滤；**

**2、关于UE中的表情使用，这个功能需要联网；**

**3、关于图片上传，该功能需要配置，配置文件在ue/php/config.json，需要指定路径**

![](media/e6f2ef86cfc3a5a3c82633f02200720d.png)

使用UE进行数据的增加结果：

![](media/87a0a2ad757883cdc41577160c06a8d7.png)

在读取的时候需要将数据表中实体字符进行还原，可以使用函数**htmlspecialchars_decode**。

<br>三、ThinkPHP中的功能类-上传类
=================================

1、介绍
-------

上传文件的一个核心操作：移动临时文件（move_upload_file）。

在ThinkPHP中系统为了方便使用，封装了一个上传类：Upload.class.php。

方法：

构造方法：

![](media/f8b14f486fe0d397139713602fcb4215.png)

可以在实例化的时候传递一个配置数组，由内部进行合并配置操作。

GetError方法：用户获取最后一次上传的错误信息

![](media/be781e3d98969271c9fcf11ca33ed2ab.png)

语法：**\$upload -\> getError();**

UploadOne方法：

![](media/4587748cfddc645a9a8210169ab1fecf.png)

参数是\$_FILES中的子元素。返回值是上传的结果。（**一种形式成功返回的时候具有九个元素一维数组，失败的时候返回false**）。

Upload方法：上传多个文件

参数通常是\$_FILES整个数组，返回值上传的结果，是二维数组，失败返回false。

![](media/5010348c474943208b0d89e55ef7d19d.png)

2、完善公文添加中附件上传
-------------------------

**注意点：**

**第一：表单要有enctype属性**

**第二：表单中的文件域type类型必须是file**

**第三：表单提交方式必须是post**

![](media/127e0fe42409795a91466590f24fb537.png)

**第一步：修改add方法中的表单数据处理部分**

为了符合MVC的设计规范，我们需要自定义一个模型，然后将文件上传以及数据的保存在模型中封装一个方法，由这个方法执行数据的保存。

创建模型文件：DocModel.class.php

![](media/9e968e900d1765630a585a15c73b6f6b.png)

编写方法，实现数据的保存。方法名叫做saveData：

![](media/ef9c7875e62fe92d5899985163a4dd1f.png)

**第二步：正式处理文件上传操作**

打印\$_FILES[‘file’]的结果：

![](media/1608b88db12ec0ce548cded2c0af1310.png)

**关于路径的说明：**

**如果地址是给服务器端脚本使用的，则可以使用相对于入口文件的相对路径，也可以使用带盘符的绝对路径。**

**如果地址是给客户端浏览器用的，则地址应该写成“/”形式，相对于站点域名后面。**

在上传的案例中整个路径都不会传递给客户端。，则属于上述的第一种情况。在上传的时候，保存路径建议写成带盘符的形式。

在开发的时候可以将带盘符的绝对路径进行拆分：

例如：D:\\WWW\\itcast\\01_1006\\Public\\Upload

可以拆分成：D:\\WWW\\itcast\\01_1006（工作目录） \\Public\\Upload（上传根目录）

而工作目录可以由魔术常量__DIR__表示，则上述的2个路径都可以用常量来表示。

常量可以在入口文件中定义：

![](media/af1b24cd908c0d1af6e574c5294474e1.png)

打印上传结果：

![](media/f2b2ed4f8dce5c10b72b7f3e18d3b95c.png)

特别注意：在保存上传文件的路径的时候，在数据表中千万不要写带盘符的路径，因为上传的文件一般都要被浏览器使用，如果使用了带盘符的路径，则会导致http协议和file协议冲突。

![](media/f4f5a2b852a8c5af2c634b32dbb4b3ef.png)

**说明：如果后期再写CURD操作的时候，只是简单的基本操作，则可以直接写在控制器中，如果数据需要处理，则最好是写在模型中进行数据的CURD操作。**

![](media/69dc08dfba75d49c594e4ca55591f218.png)

3、实现公文列表的附件下载
-------------------------

**第一步：展示文件的信息，修改模版文件showList**

在列表中可以展示出数据表中的filename（原始的文件名）

![](media/4c8369586437b0abb295cf6f661dd2e3.png)

**第二步：在附件后面添加一个下载按钮，点击实现下载**

分析：如果有附件，则可以显示下载按钮，如果没有的话则不要显示。

**有没有附件可以取决于hasfile字段（0表示没有，1表示有），可以是if标签进行判断**：

![](media/541f793a5da047b19ec87c9abacbc14d.png)

**除了使用hasfile字段，我们还可以通过filepath、filename字段进行判断，如果不为空，则表示有附件：**

此时可以使用另外一个标签：empty或者notempty标签

![](media/d47ef705838f4f2ac305dc0fa3ef7f32.png)

所以上述的if标签代码，还可以写成：

![](media/5c9b84a137dc0aa07f697801515eb809.png)

编写下载方法download：

-   **\$file = "D:/Uploads/photo.jpg";**

-   **header("Content-type: application/octet-stream");**

-   **header('Content-Disposition: attachment; filename="' . basename(\$file) .
    '"');**

-   **header("Content-Length: ". filesize(\$file));**

-   **readfile(\$file);**

![](media/b0a7d835f4871456901722d1b5b89532.png)

显示效果：

![](media/d04ec66896ecd2d8da12c9a686344c38.png)

四、layer
=========

1、介绍
-------

Layer是一款基于jQuery开发的插件，作用是用于美化弹窗的效果。

官网：<http://layer.layui.com/>

在线手册：<http://www.layui.com/doc/modules/layer.html>

![](media/0901387738a5ed56ca387f1336126ba2.png)

下载之后会得到一个压缩包：

![](media/2c2a0c378d465dad5b31d54afd5a1bf1.png)

经过精简之后只剩下一个javascript文件和一个css文件以及一张图片：

![](media/ec06dd3575a77d98ea6156105673aadd.png)

**使用步骤：**

**第一个：引入javascript文件（jQuery文件+layer.js，先引入jQuery文件）；**

**第二个：参考官网的demo来编写javascript代码就可以了。**

2、使用layer实现查看公文的功能
------------------------------

案例要求：点击公文后面的【查看】按钮，弹出窗口显示公文内容（content字段）。

**第一步：将layer目录（包含了layer.js和skin目录）复制到插件目录下**

![](media/de1df31700b9d33efdecbbce79fc7fc2.png)

**第二步：在页面中引入layer.js和jQuery的javascript文件**

![](media/e5db89132653ace7ffb38365e67890e4.png)

测试layer使用：

测试代码：layer.alert(‘hello world.’);

![](media/993d0aa4276b2dde22d14050e612cc36.png)

**第三步：给【查看】按钮绑定点击事件**

![](media/97f51299e8af67e5fe42e08965b674cf.png)

传递公文的标题：

![](media/f93c7f7bb9c6857bf19bd6d8032710c5.png)

给查看按钮添加一个选择器，并且在点击显示内容的时候需要告知服务器我们需要查看的公文id，id我们可以通过自定义html属性的方式来传递，然后通过jQuery的attr方法获取属性的值（也就是id）：

![](media/0172f3b430ba17ef1a248426d3640b1c.png)

demo代码：

1.  //iframe层

2.  layer.open({

3.  type: 2,

4.  title: 'layer mobile页',

5.  shadeClose: true,

6.  shade: 0.8,

7.  area: ['380px', '90%'],

8.  content: 'http://layer.layui.com/mobile/' //iframe的url

9.  });

目前的方法能够实现弹出效果，但是里面的内容不是我们想要的内容，所以此时需要编写方法展示公文的内容：

方法名：showContent

![](media/202056c72838467e061698df69c93a19.png)

方法代码：

![](media/f827d0014fa3c2cf20a8c461660399c5.png)

显示效果：

![](media/b076b734f7508c83a4049694042739e7.png)

<br>五、扩展（2）
=================

在ThinkPHP中获取ip信息扩展
--------------------------

在ThinkPHP中系统封装了一个方法来获取ip：get_client_ip()【系统函数库文件中】

语法：

**Get_client_ip(可选参数数字)**

如果参数是0的话或者不写（默认），则表示返回正常的ipv4地址；

如果参数是1的话则表示返回ipv4地址对应的数字地址。

关于数字地址和ip地址的计算方法：

![](media/45807f843c9bd695dd7a9c7c895f4c53.png)

**重点是如何将ip地址转化成物理地址？**

什么是物理地址？

物理地址就类似于：

![](media/ff9dd1d5a9da3ad8aab8fde048566cd8.png)

在ThinkPHP中系统提供了一个工具类，能实现转化，但是系统不提供转化所使用的数据，也就是说需要自己去寻找对应的数据库。

数据库可以从纯真官网去寻找（<http://www.cz88.net>）

![](media/cca80dac8c12f1f3f8a47d4d843d79ef.png)

下载安装的程序之后在其安装目录中可以找到qqwry.dat文件：

![](media/3f3b51c4d5be7bd3c7517203e480595f.png)

该文件就是后续所使用到的数据库文件。

ThinkPHP中提供的类：Iplocation.class.php

![](media/f440c2e0e2c18413bd1db653f752220e.png)

构造方法：

![](media/1e64b68fe778875b250897bba3184c68.png)

可以得知，在实例化的时候可以传递一个文件名，文件名所在的位置和当前的类是同级目录。

Getlocation方法：查询，需要传递ip地址，如果为空则表示查询当前用户的ip地址

![](media/6ab64a6596f3047baa5ff6b1db7ae725.png)

将数据库文件复制到指定的目录

![](media/5bd1ed0941ae86c5abecc7ee868c913e.png)

编写代码：

![](media/5cb4ea217023eba03dfaaf5df7971280.png)

![](media/f372174c6fe84dd1277fb5c38075b88f.png)

接口写法：

![](media/c9d43995b4d8be02b301fc47e0c74079.png)
