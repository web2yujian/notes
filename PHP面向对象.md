# PHP面向对象

## 一、大纲

> ### 基础

1. **类的创建【构造函数】【析构函数】**
2. **类的属性和方法【访问修饰符`public `  `protected`  `private`  】**
3. **静态属性和方法**
4. **魔术方法【属性的重载】【方法的重载】**

> ### 高级

1. **继承**

2. **其他【`requrie`  `include`】【命名空间】**

   #### 

## 二、基础

### 1. 类的创建

- **构造函数和析构函数**

```php
class 类名{
   
  function __construct() {
      //构造函数
   }

   function __destruct() {
      //析构函数
   }
    
}
```

- **构造函数作用**

  > 初始化对象    ------实例化对象之后就会调用构造函数

- **析构函数作用**

  > 对象的销毁   ------析构函数会在到某个对象的所有引用都被删除或者当对象被显式销毁时执行。


### 2. 类的属性和方法

- **访问修饰符**    `public `  `protected`  `private`

  - public

    > class 外部也可以访问

  - private

    > 仅仅 可以在类的内部被调用

  - protected

    >可以在类的内部和其的子类中被调用

- **属性**

  ```php
  class Car{
  
    public $color;     //定义属性
  
  }
  ```

- **方法**

  ```php
  class Car{
  
    public $color;     //定义属性
    
    private $price;	 
  
    public function getPrice(){
    
        echo $this -> price;
        
    }
    
    
     function __construct() {
        //构造函数
        $price = 10000;
     }
  
     function __destruct() {
        //析构函数
     }
  
  }
  ```


### 3. 静态属性和方法

> #### **定义** ：在属性或方法前加 `static` 关键字，即为静态属性

- **为什么要用 `static`**

  > 在实际工作中会有一个类的多个对象，可能会共享一份数据。

  ```php
  class Circle{
      //定义圆形的圆周率 常量PI
      const PI = "3.14";
  }
  ```

  > 如上所示，常量的使用解决了“共享”的问题，但是**类常量不能更改**，**有时在共享一份数据后，还要所有的共享此数据的对象还允许更改**,于是就出现了`static`

- 调用静态属性和方法

  - `类名::属性`    `类名::方法()`
    - 如：

  ```php
  <?php
  
  class Circle{
      //定义圆形的圆周率
      public static $PI = "3.14";
  
      public $radius = 3;
  
  }
  //实例化对象
  $cir = new Circle();
  //调用半径
  $radius = $cir ->radius;
  //获取圆周率并且更改   (类名::属性)
  Circle::$PI = 3.1415;
  $PI = Circle::$PI;
  
  echo "The area of the circle is".( $PI*pow($radius,2));
  ```



  > 观察上述代码，会发现static属性可以更改

  > 注意：
  >
  > - 静态属性与类常量相似(相同)，唯一的区分是类常量不可以更改，静态属性可以更改。访问方法是一样的。
  >
  > - `::` 只能访问类常量、静态属性、静态方法
  >
  > -  静态属性需要加`$`，常量名前没有`$`

- 静态方法中，`$this`伪变量不可以使用

  ```php
  <?php
  class Circle{
      //定义圆形的圆周率
      public static $PI = "3.14";
  
      public $radius = 3;
  
      public  function area(){
          $radius = $this ->radius;
          $PI = Circle::$PI;
          //调用静态的say()方法时，不能使用$this，应当使用self::say()
          echo self::say().( $PI*pow($radius,2));;
      }
  
      public static function say(){
          return "The area of the circle is";
      }
  }
  //实例化对象
  $cir = new Circle();
  //调用函数获取面积
  $radius = $cir ->area();
  ```


### 4. 魔术方法



## 三、高级