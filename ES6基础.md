# ES6基础

# 一、块级作用域

## 1. var

首先看看ES5中得变量声明方式

```javascript
if (true) {
	var a = 2
}
console.log(a) // 2
```

以上代码等同于

```javascript
var a
if (true) {
	a = 2
}
console.log(a)
```

>  以上可知 ：
>
> 1. 在块内部定义变量 变量提升，到函数最顶部
> 2. 通过var声明的变量，无论在何处声明，均为**全局作用域**



## 2.let 和 const

再来看看`ES6`中的`let`和`const`

### `let`

```javascript
if (true) {
	let b = 2
}
console.log(b) // b is not defined
```

>  此时在{} 外部访问b 将会报错，因为 let 的作用域仅为 `{ } `的内部，及**块级作用域**

### `const`

```javascript
if (true) {
	const c = 2
}
console.log(c) // c is not defined
```

> 从上面可知 const 也是也仅为块级作用域
>
> **const的作用域与let作用域相同：只在声明所在的块级作用域内有效**

让我们看看const 更多的特性：

**const 表示常量：**

```javascript
const d = 2
d = 3 // Assignment to constant variable.
```

> 此时，当 d 为 **基本数据类型**的时候，改变其值，将会报错！！！

**但是它的常量仅仅表示的是地址常量 对象的成员可以改变值**

看看下面的例子：

```javascript
const people = {name: '张三', age: 23}
people.age = 25
console.log(people) // {name: "张三", age: 25}
```

看看此时 **`people`**已经被改变了

**why?**

> 对象是复杂的数据类型 它的地址保存在 栈里面， 值保存在堆里面
>
> cosnt仅仅是保证这个地址不改变，至于地址对应的数据，是可以进行改变的
>
> 基本类型值在内存中占据固定大小的空间 因此被保存在栈内存中。比如 const a = 1 ; 这时候其直接保存在栈里面





# 二、字符串

## 1. 字符串拼接

### ES5中字符串拼接

```javascript
// ES5 
var name = 'Hunter'
console.log('hello ' + name)
```

### ES6中字符串拼接

```javascript
// ES6
let name = 'Hunter'
console.log(`hello ${name}`) // hello Hunter
```

**注意**：用 `${}`来拼接字符串，注意此时要使用 ` `` `（反单引号）; 如下所示： 单引号将无法将其转义

```javascript
console.log('hello ${name}') // hello ${name}
```

### ES6的字符串换行

```javascript
// ES5
    var template = "<div> \
                        <span>hello world</span> \
                    </div>"
// ES6
    let template2 = `<div> 
                        <span>hello world</span>
                    </div>`
```

> ES5中需要用反斜杠来进行多行字符串拼接，ES6直接使用 ` `` `(反单引号）



## 2. 字符串方法

### padStart() 和 padEnd()

>  ES6 引入了字符串补全长度的功能，如果某个字符串不够指定长度，会在头部或者尾部补全。
>
>  `padStart()` 用于**头部补全**；
>
>  `padEnd()` 用于**尾部补全**。

如下一个例子：[例子来源](https://www.jianshu.com/p/287e0bb867ae)

```javascript
 setInterval(() => {
        const now = new Date()
        const hours = now.getHours().toString()
        const minutes = now.getMinutes().toString()
        const seconds = now.getSeconds().toString()
        console.log(`${hours.padStart(2, 0)}:${minutes.padStart(2, 0)}:${seconds.padStart(2, 0)}`)
    }, 1000)
```

> 先不管箭头函数

看看其中的`hours.padStart(2,0)` , 表示当小时不够两位数时，在前面补0，如`8`，补充成 `08`

后面遇到更多的字符串函数会补充



  **结合网上的内容，个人理解而得 欢迎指正**



# 三、函数

## 1. 参数默认值

### `es5中参数默认值设置`

```javascript
  // ES5
  function show (num) {
      num = num || 100
      console.log(num)
  }
  show(20) // 20
```

但是当传递的参数为0时：

```javascript
show(0) // 100
```

> 控制台打印 100 
> 因为此时的 0 作为参数，当作false处理， false || 100 === 100

这不是我们想要的，所以看看ES6中怎么解决的

### `ES6`中参数默认值设置

```javascript
 function show (num = 1000) {
 	console.log(num)
 }
 show(0) // 0
 show() //100 默认值
```

此时输出了我们想要的 0

## 2. rest (剩余参数)

> ES6 引入 rest 参数（形式为`...变量名`），**用于获取函数的多余参数**，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。(来源：[阮一峰博客](http://es6.ruanyifeng.com/#docs/function#rest-%E5%8F%82%E6%95%B0))

### ES5中的arguments

>  `arguments`**并不是数组**

```javascript
arguments instanceof Array // false
```

> `arguments`是一个类数组对象，它包含length属性。

```javaScript
arguments instanceof Object // true
```

> 我们可以通过`Array.prototype.slice.call(arguments)`将获取对应真实数组。

### ES6中的rest

> `rest`是一个真实数组

```javascript
rest instanceof Array // true
```

### 万物皆对象

当然` rest` 也是 对象

```javascript
rest instanceof Array // true
```

