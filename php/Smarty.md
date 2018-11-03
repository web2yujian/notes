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

#### 3.基本实现

- 配置

  `test.php`

  ```php
  <?php
  //1.Smarty类的引入  引入上图的主文件
  require '../libs/Smarty.class.php';
  
  //2.Smarty类的实例化
  $smarty = new Smarty();
  
  //3.Smarty  "五配置两方法"
  $smarty -> setLeftDelimiter('{');         //左定界符
  $smarty -> setRightDelimiter('}');        //右定界符
  $smarty -> setTemplateDir('tpl');         //html模板的地址
  $smarty -> setCompileDir('template_c');   //模板编译生成的文件
  $smarty -> setCacheDir('cache');          //缓存地址
  
  //Smarty的缓存机制不太理想，可以不使用
  $smarty -> setCaching(Smarty::CACHING_LIFETIME_CURRENT);
  $smarty -> setCacheLifetime(300);
  ```


- 基本操作

  `test.php`

  ```php
  //1.注册
  $smarty->assign('title','学习Smarty');
  
  /*也可以分开
  $title = "学习Smarty";
  $smarty->assign('title',$title);
  */
  
  //2.展示模板
  $smarty->display('test.tpl');
  ```

  `test.tpl`

  ```php+HTML
  {$title}
  ```

  > 以上实现了一个简单的模板注册数据以及展示数据



  **总结步骤：**

    Step 1：加载 Smarty 模版引擎。  
    
    Step 2：建立 Smarty 对象。 
    
    Step 3：设定 Smarty 对象的参数。 
    
    Step 4：在程序中处理变量后，再用 Smarty 的 assign 方法将ji变量置入模版里。 
    
    Step 5：利用 Smarty 的 display 方法将网页显示出来


## 三、Smarty模板的设计
#### 1.模版注释

​	模板注释被号包围，例如 **{* this is a comment *} **

​	定界符可以改变，如果定界符改为`<{` 和 `}>`

​	则注释为    **<{* this is a comment *}>**

#### 2.保留变量

​	在Smarty模板中使用保留变量时，无须使用assign（）方法传值，直接调用变量名即可。      

​        smarty中常用 的保留变量：

~~~php
```php
{$smarty.now}            //取得当前时间戳
{$smarty.const}          //直接访问php常量
{$smarty.capture} 		 
{$smarty.config}         //取得配置变量
{$smarty.section} 
{$smarty.template} 
{$smarty.current_dir} 
{$smarty.version} 
{$smarty.block.child} 
{$smarty.block.parent} 
{$smarty.ldelim},  
{$smarty.rdelim}
```
~~~

> **自行百度**



#### 3.变量调节器

- `capitalize` (首字母大写)

  继续在代码实现：

  `test.php`

  ```php
  //1.注册数据
  $smarty -> assign('habbit','i like eat apple');
  
  //2.展示模板
  $smarty -> display('test.tpl');
  ```

  `test.tpl`

  ```php+HTML
  {$habbit|capitalize}
  ```

  效果展示：

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181029165949.png)

  > 可以看出每个单词的首字母大写了

- date_format （转换时间戳格式）

  `test.php`

  ```php
  $smarty -> assign('date',time());
  ```
  `test.tpl`
  ```php
  {$date|date_format}
  ```

  > 效果是将时间戳格式转换为我们可读的年月日

  ```php
  {$date|date_format:"%B %e, %Y"}
  ```

- default  （默认展示）

  `test.php`

  ```php
  //定义一个变量模拟 个人签名 为空的时候
  $signifcant = "";
  $smarty -> assign('signifcant',$signifcant);
  ```

  `test.tpl`

  ```php
  
  ```


效果展示：

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181029172101.png)

如果`$significant`不为空

```php
$signifcant = "哥只是个传说";
```

效果展示：

![1540804977201](C:\Users\10482\AppData\Roaming\Typora\typora-user-images\1540804977201.png)

> 从以上三个变量调节器中，我们了解到了**变量调节器**的作用以及用法

 后面的粗略列出：

- escpae

  > 用于html转码，url转码，十六进制转码等。详见手册

- lower/upper

  > 将变量字符串小（大）写

- nl2br

  > 所有换行符转换成 `<br/>`

- .......(后面自己看手册)



#### 4.流程控制

- **条件判断**

  - 基本句式

    ```php
    {if $name eq "Fred"}
       Welcome Sir.
    {elseif $name eq "Wilma"}
       Welcome Ma'am.
    {else}
       Welcome,whatever you are.
    {/if}
    ```

  - 基本的条件修饰符：
    - eq    (==)
    - neq  (!=)
    - gt      (>)
    - lt       (<)

  >  **注意：**修饰词必须和变量或常量用空格隔开

  - 案例

  `test.php`

  ```php
  $score  = 59;
  $smarty -> assign('score',$score);
  ```

  `test.tpl`

  ```php
  {if $score gt  90}
    优秀
  {elseif $score gt 59}
    合格
  {else}
    挂科啦
  {/if}
  ```

  效果展示：

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181029190307.png)

   - **Smarty 的循环语句 section**

     - 尝试使用

     ​	`test.php`

     ```php
     $arr2 = array(
         array(
             'title'  => 'Smarty的学习',
             'author' => '小明'
         ),
         array(
             'title'  => 'html的学习',
             'author' => '小红'
         )
     );
     $smarty -> assign('arr2',$arr2);
     ```

     ​	`test.tpl`

     ```php
     {section name=arrList loop=$arr2}
       {$arr2[arrList].author}
       {$arr2[arrList].title}
     {/section}
     ```

 ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181030102225.png)



- 以上是表格其他 section 的参数

   - **foreach**

     - 可用于循环关联数组

       `test.php`

       ```php
       $arr2 = array(
           array(
               'title'  => 'Smarty的学习',
               'author' => '小明'
           ),
           array(
               'title'  => 'html的学习',
               'author' => '小红'
           )
       );
       $smarty -> assign('arr2',$arr2);
       ```

       ​	`test.tpl`

       ```php
       {foreach item=arrList from=$arr2}
         {$arrList.title}
         {$arrList.author}
         <br>
         {foreachelse}
         当前没有内容
       {/foreach}
       ```

       ` {foreachelse}`  。同时，`{section }` 也支持 `{sectionelse}`

       不赘述。

     - 在**Smarty 3**之后，**支持php原生的foreach 语法**

       ```php
       {foreach $arr2 as $arrList}
         {$arrList.title}
         {$arrList.author}
         <br>
       {/foreach}
       ```


#### 5.Smarty文件的引入

- **include**

  先创建一个`header.tpl`  文件，待引入，写简单的一句话

  ```php
  我是 header.tpl
  ```

  然后到 `test.tpl` 中去引入

  ```php+HTML
  {include file="header.tpl"}
  ```

​	效果如下：

​	![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181030110109.png)

 	`include` 除了 `file` 属性之外，还有其他自定义的属性

​	 比如创建一个属性`sitename` 用他表示网站名称

​	  	

```php
{include file="header.tpl" sitename="github"}
```

​		这时候 `header.tpl` 里面就可以输出 sitename 的属性

```php
{$sitename}
```



- **Smarty类与对象的复制与使用**

  - register_object方法，在Smarty中已经弃用

  - assign方法；将一个类的对象以变量的形式复制到smarty模板中使用

    `test.php`

    ```php
    class A{
      function meth1(){
          echo "hello";
      }
    };
    
    $a = new A();
    $smarty->assign('a',$a);
    
    $smarty -> display('test.tpl');
    ```

    `test.tpl`

    ```php
    {$a -> meth1()}
    ```

  > 这样就能输出   hello   的字样


#### 6.函数的使用

- php内置函数

    `test.php`

  ```php
  $smarty -> assign('time',time());
  $smarty -> display('test.tpl');
  ```

  `test.tpl`

  ```
  {"Y-m-d"|data:$time}
  ```

前面"Y-m-d"是作为函数data()的第一个参数，冒号后面时data()的第二个参数

>  打印出时间

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181101105036.png)

- 自定义函数

  - register

    ```
    $smarty -> registerPlugin('function','f_test','test);
    ```

#### 7.function函数库的定义和使用

​	![](https://raw.githubusercontent.com/HunterXing/resourse/master/20181101111634.png)





#### 8.modifies变量调节器插件的定义和使用

#### 9.block(区块插件)



## 四、Smarty程序设计

