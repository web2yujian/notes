# JavaScript检测数据类型

# 1.`typeof`

>  **`typeof `操作符是确定一个变量是`String`、`Number`、`Boolean`、`undefined`的最佳工具**

**来源：《JavaScript高级程序设计》图灵程序设计丛书**

看下面例子：

```javaScript
var s = 'hello';
var num = 10;
var bool = true;
var und;

typeof s;    // "string"
typeof num;  // "number"
typeof bool; // "boolean"
typeof und;  // "undefined"
```

> ok，都检测出来了，but, 如果检测的是一个对象或者null,皆会返回`Object`

```javaScript
var n = null;
var o = new Object();

typeof n; // "object"
typeof o; // "object"
```

**看吧，一点区分度也没有。**

> 所以： 在**检测基本数据类型**时，typeof很好用，
>
> 在检测**引用类型的值**时，typeof的作用不大



# 2.`instanceof`



```javascript
var o = new Object();
var arr = [];
var reg = /^abc$/

o instanceof Object   //true
arr instanceof Array  //true
reg instanceof RegExp //true
```

**注意:使用`instanceof`操作符检测基本数据类型的值时，都会返回`false`,尽管下面的例子看起来很矛盾**

```javascript
null instanceof Object // false
typeof null // "object"
```



# 3.`Object.prototype.toString()`

 [ECMA-262](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf) 规范中，`toString`方法是这样定义的:

- 如果参数是未定义的值，则返回`"[object Undefined]"`.
- 如果参数为null，则返回`"[object Null]"`.
- 如果适用ToObject函数传递参数，则返回对象.
- 如果参数为类，则返回包含对象的类.（Let class be the value of the [[Class]] internal property of O.）
- 返回一个由"[对象", 类, 和"]"拼接而成的字符串.

> 它可以返回引用类型更精准的类型检测

```javascript
var o = new Object();
var arr = [];
var reg = /^abc$/

Object.prototype.toString.call(o) // "[object Object]"
Object.prototype.toString.call(arr) // "[object Array]"
Object.prototype.toString.call(reg) // "[object RegExp]"

```

通过函数封装处理一下：

```javascript
var type = function (o) {
    var s = Object.prototype.toString.call(o);
    return s.match(/\[object (.*?)\]/)[1];
}
type(o) // "Object"
type(reg) // "RegExp"
type(arr) // "Array"
```

