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





# 三、变量的解构赋值

```javascript
// ES5
let a = 1;
let b = 2;
let c = 3;
```

## ​1.ES6数组解构赋值

```javascript
let [a,b,c] = [1,2,3];
console.log(`${a} ${b} ${c}`) // 1 2 3
```

### 默认值​

```javascript
let [d = 2, e] = [undefined, 3];
console.log(`${d} ${e}`) // 2 3
```

> 当赋值为`undefined`时取默认值 当赋值为其他的有效值或者`null`时 取所赋值的值

```javascript
let [f = 2, g = 3] = [null, 4];
console.log(`${f} ${g}`) // null 4
```



## 2.对象解构赋值

​        let {foo, bar} = {foo: 'hi', bar: 'hello'}

​        console.log(`${foo} ${bar}`) *// hi hello*

​        *// 总结： 数组按照顺序解构 对象按照key值进行解构*

​        let soso;

​        *// { soso } = { soso: "hi"}; // 错误*

​        ({ soso } = { soso: "hi"}); *//得加上圆括号 ()*

​        console.log(soso) *// hi*

​        *// 注意：先定义再解构需要在解构语句那块加上圆括号*

​        

## 3.字符串的解构赋值

​        const [h,i,j,k,l] = 'hello';

​        console.log(`${h} ${i} ${j} ${k} ${l}`)