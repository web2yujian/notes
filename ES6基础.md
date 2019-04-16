# ES6基础

### 一、块级作用域

#### 1. var

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



#### 2.let 和 const

再来看看`ES6`中的`let`和`const`

##### `let`

```javascript
if (true) {
	let b = 2
}
console.log(b) // b is not defined
```

>  此时在{} 外部访问b 将会报错，因为 let 的作用域仅为 `{ } `的内部，及**块级作用域**

##### `const`

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

  **结合网上的内容，个人理解而得 欢迎指正**

