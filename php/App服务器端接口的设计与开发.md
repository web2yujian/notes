# APP服务器端接口设计与开发

## 一、接口概述

1. #### **概念**

   硬件的接口用于连接不同硬件，它看得见摸得着，因此很容易理解。在软件开发中，为了实现软件不同部分之间的交互，也需要使用接口。

   我们现在都习惯于在网上充值话费、查看天气、还信用卡、缴费等等。例如，下图是我们常见的天气预报页面，我们只要选择不同的城市，页面就能显示当前城市最新的天气预报甚至最近七天的天气。

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028091828.png)

   事实上，提供天气预报数据的肯定不是各个软件开发者，而是国家气象局。气象局把全国天气预报查询功能加以封装，对外发布一个对接窗口，所有想使用本功能的其他软件只要调用这个对接窗口，即可得到天气预报数据，再显示即可。

   对于该功能是如何实现的，对使用者来说是透明的，也无需关心。这种为了实现软件不同部分之间的交互，所设计出来的对接窗口，就是所谓的软件接口，即**API（Application Programming Interface,应用程序编程接口）。**

2. #### **不同的平台之间遇到的问题**

   我们在开发普通软件时，因为使用的是同一种语言，在传递数据（变量，数组，对象等）时，可以使用相互认识的数据结构进行传递。

   在移动开发领域，手机端APP开发技术主要有：Android和IOS，服务器端开发主要是：PHP、.NET、JSP，手机端APP要跟服务器端连接传递数据，会有什么问题呢？

   ![blob.png](http://iflyssedata.oss-cn-shanghai.aliyuncs.com/upload/image/20161121/6361532332087213385749771.png)

   - 1）手机端和服务器端开发语言不一样，对数据定义的标准不一样。

   - 2）数据传递时，数组、对象格式的数据无法互相传递。

   - 3）数据格式不统一，无法解析对方的数据。

3. #### 如何解决

   - 如何解决app端与服务器端数据交互的问题呢？

     先看一个问题。如果我们通过天气预报服务器接口获取到了苏州的天气： 

     `**苏州阴16~20185060%**

     看看怎么解析=====> 城市：苏州，天气：阴，温度范围：16~20，然后……185060%是什么呢？

     别人家的数据，我们理解不了！！![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028092310.png)

     因此，我们需要制定一种及其简便易用并且统一的数据格式用于在网络中传输，于是，在21世纪初，道格拉斯·克罗克福特（Douglas Crockford）发明了一种叫做**JSON**的超轻量级的数据交换格式。如果输出的数据格式变为以下的方式，你是不是立刻就能理解了呢？

     ` "城市":"苏州","天气":"阴","温度范围":"16~22","当前温度":18,"PM2.5":"50"`

     这些数据都能“自我描述”，即使没学过任何编程知识，我们都能理解，因为它是“**人类可读的**”。

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028092346.png)



   - 对于数组、对象之类的数据，如何定义统一的格式呢？



     > 1）服务器端：发送数据时，把数组数据用[]包装，把对象使用{}包装.
     >
     > 2）APP端：接收数据时，把[]包含的数据转换为数组，把{}转换为对象。



     假设苏州的一条天气预报信息为一个对象，我们可以这样组织数据：

     `{“城市”:”苏州”,”天气”:”阴”,”温度范围”:”16~22”,”当前温度”:”18,”PM2.5”:”50”}  `

4. #### **PHP服务端接口**

   我们来看一下APP客户端和服务器端交互的运行机制：

   假设PHP源文件city.php，已实现天气预报功能。即city.php为天气预报功能模块。 

   1）当APP客户端想要调用该功能模块时，只要发送请求（服务器IP地址+功能模块文件），即http://www.weather.com.cn/city.php。

   **2）服务器端接收到请求，获取请求数据，执行city.php源文件，再把结果（包含数据）返回给客户端。**

   3）客户端接收数据，在页面显示。



   *以上只有（**2）是我们PHP服务器端接口开发需要关注的内容，***

   *（1）和（3）均由APP客户端处理。*





   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028093120.png)

5. #### 实现

   要求实现就是类似于city.php这样的特定功能，它跟我们编写普通的PHP代码基本一样，其特点为：



   1）city.php页面不需要展示，它只关注功能实现，并发送给用户想要的数据。

   2）city.php输出的数据格式比较严格，为JSON(XML也可以，但不作为本次知识点)。

   3）city.php获取数据也是使用$_GET、$POST、$REQUEST等方式实现。

   4）city.php发送数据使用echo实现。



   ![blob.png](http://iflyssedata.oss-cn-shanghai.aliyuncs.com/upload/image/20161121/6361533803971050956289824.png)

   天气预报功能模块作为桥梁，连接了服务器端与用户端，使得它们相互之间可以交互，这就是所谓的软件天气预报接口。即连接软件不同部分的交互接口。

   *请记住，从程序员角度来看，**所谓的接口，就是一个PHP源文件。只不过它有输入，也有输出。***

## 二、JSON基础

1. #### **JSON的概念**

   在编写PHP服务器端接口之前，我们有必要先要了解一下数据的输出格式，即JSON。

   ![blob.png](http://iflyssedata.oss-cn-shanghai.aliyuncs.com/upload/image/20161121/6361534421176732764384973.png)



   没错，我们之前已经接触过了，例如：

   `{"城市":"苏州","天气":"阴","温度范围":"16~22","当前温度":"18","PM2.5":"50"}`

   - JSON是一种轻量级的文本数据交换格式，其全称为：`JavaScript Object Notation`（JavaScript 对象表示法） 。
   - JSON不是一种编程语言，它只是制定了一系列的规则，用于规范数据的格式。 
   - JSON实际上是JavaScript的一个子集。(JSON的设计者：道格拉斯·克罗克福特（Douglas Crockford），他长期担任雅虎的高级架构师，十分钟情于JavaScript。)
   - JSON的特点：

      ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028094119.png)

   **下表是XML和JSON特点的比较，打“√”的，说明更胜一筹。**

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028094608.png)

2. #### **JSON的语法结构**

   **案例**

   > 小明同学的个人信息为：性别男，18岁，身高1.72米，年级未知，精通JavaScript、PHP、JAVA。
   >
   > 使用JSON如何格式化小明同学的数据？

   ```php
   {
     "name":小明,
     "age":18,
     "gender":true,
     "height":1.72,
     "grade":null,
     "skill":[
       "JavaScript",
       "Java",
       "PHP"
     ]
   }
   ```

   > JSON语法规则非常简单，四句话就能概括出来，而且道格拉斯·克罗克福特（Douglas Crockford）声称这个规格永远不必升级，因为该规定的都规定了。

   ![blob.png](http://iflyssedata.oss-cn-shanghai.aliyuncs.com/upload/image/20161122/6361540518352238488482011.png)

   - **注意**

     需要注意的是：

     > 1）逗号避免使用中文逗号
     >
     > 2）最后一个数据不需要使用逗号

3. #### **JSON与PHP数组**

   - PHP数组

     我们都知道，使用PHP编写的功能代码中，数据会保存于各种变量、数组以及对象中。



     *例如：小明同学的个人信息为：姓名小明，性别男，18岁，身高1.72米，年级未知*



     使用PHP代码如何实现数据的保存呢？



     1）把所有数据均通过变量保存：

     ```php
     $name="小明";
     $age=16;
     $gender=true;
     $height=1.72;
     $grade=null;
     ```

     2）使用关联数组

     ```php
     $student1 = array(
         
       "name"   => "小明",
     
       "age"    => 16,
     
       "gender" => true,
     
       "height" => 1.72,
     
       "grade"  => null
     );
     
     ```

     上述两种方法，很明显，方法2更加合理，数组不仅保证了数据的完整性，还增加了可读性

     **PHP数组保存数据的格式跟JSON格式十分相似，因此关联数组中的数据转换为JSON格式应该是很简单的事。**

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028100232.png)



     1）把关联数组中的右箭头“=>”变为JSON表示的冒号“：”

     2）把数组中的数据用{}括起来。

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028100259.png)

   - **从PHP5.2开始，PHP原生提供了json_ecode()函数，用于将数组或对象等转化为JSON格式的字符串**

   ```php
   <?php
   
   $book = array(
       
     "name"  => "PHP",
       
     "price" => 35
       
   );
   
   $json = json_encode($book);
   
   echo $json;
   ```

   运行结果：

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028100953.png)

   **中文格式**

   将存储小明个人信息的数组转换为JSON格式，其PHP代码如下：

   ```php
   $student1=array(
       "name"   =>"小明",
       "age"    =>16,
       "gender" =>false,
       "height" =>1.72,
       "grade"  =>null
   );
   
   $json = json_encode($student1);
   
   echo $json;
   ```







   问题：转换后的JSON格式数据中，中文汉字没有正常显示，而是显示"\u0421"，这是什么原因呢？

   这是因为使用json_ecode()函数转换后的数据，编码格式会由utf-8格式转换为unicode格式，显示的\u格式就是汉字的显示形式。

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028101556.png)

   如何解决呢?

   1）升级PHP版本到5.4以上，`json_encode(value,option)`中第二个参数`option`设置为`JSON_UNESCAPED_UNICODE`即可转换为`utf-8格式`

   ```php
   $student1 = array(
       
       "name"   =>"小明",
       
       "age"    =>16,
       
       "gender" =>false,
       
       "height" =>1.72,
       
       "grade"  =>null
   );
   
   $json = json_encode($student1,JSON_UNESCAPED_UNICODE);
   
   echo $json;
   ```

   2）服务器端无需解决。以unicode格式发送给app客户端，app端接收数据时再做转换

   - JSON格式转换为数组或对象

     `json_decode($json[,true]);`

     - 加参数`true`为数组。 否则为对象

   ```php
   header("Content-type: text/html; charset=utf-8");//设置源文件编码格式
   
   $student1=array(
       "name"   =>"小明",
       "age"    =>16,
       "height" =>1.72,
       "grade"  =>false
   );
   
   $json = json_encode($student1,JSON_UNESCAPED_UNICODE);
   
   $php = json_decode($json,true);
   
   var_dump($php);
   ```

4. #### JSON与接口规范

   在设计接口时，必须要遵循一定的规范，这样设计出来的接口不仅在风格上保持一致，而且可以降低多个系统之间的耦合性，使用起来简单易懂，方便快捷。

   1）域名

   我们设计出来的接口，**应该尽量部署在专用域名之下。**

   *例如：https://api.example.com*

   2）路径

   路径又称"终点"（endpoint），表示接口（API）的具体网址。

   *例如：有一个API提供动物园（zoo）的信息，还包括各种动物和雇员的信息，则它的路径应该设计成下面这样。* 

   *https://api.example.com/animals*

   *https://api.example.com/employees*

   3）状态码和提示信息

   当服务器响应用户的请求时，返回的信息中应该包含状态码和状态信息，告诉用户服务器响应的结果。用户根据状态码执行不同的操作。 因此，一般返回的JSON数据中，需要添加两个键值对，用于记录状态码和提示信息。

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028111159.png)

    

   *例如：用户请求取得小明的个人信息，如果服务器成功获取，返回的完整的JSON格式应该是：*

   ​     

   ```php
    {
   
             "code"：1001，              //状态码
   
             "message":" 请求数据成功",   //状态码对应的文字消息
   
             "content"： {              //个人信息
                 
                 "name"："小明",
                 
                 "age"：16
             }
   
    }
   ```



> 接口设计时，需要考虑接口的安全性，需要防止接口被恶意刷新或黑客恶意调用，尤其是大型商业应用。因此，客户端和服务端针对不同接口统一做好加密工作，服务端在每次接口需要都要进行验证。

接口可以简单分为三种：**普通接口、表单接口、会员接口**

> 1）普通接口：用户无需登录就可以浏览的内容
>
> 2）表单接口：需要操作服务器数据库
>
> 3）会员接口：只有登录后才可以访问的内容



![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028111543.png)

其中**token就是所谓的令牌**，客户端只有持有服务器端分配的令牌，才可以正常访问服务器端接口，token的值是由服务器端生成后发送给客户端的。下图为APP客户端与PHP服务器端交互的流程图。

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028111611.png)



- #### **总结**

  使用 PHP原生函数json_ecode()函数格式化数组或对象时：



  1）PHP关联数组转换成JSON格式时，变为JSON对象。

  2）PHP索引数组转换成JSON格式时，变为JSON数组。



  使用 PHP原生函数json_decode()函数解析JSON数据时：

  1）通常情况下`，json_decode()`总是返回一个**PHP对象**

  2）如果要转换为php数组，可以在调用`json_decode`时，增加一个参数，设为`true，	` `json_decode($json,true)`



  服务器端接口功能实现的流程为：

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181028111758.png)


## 三、社区移动端接口的设计