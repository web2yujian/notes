# ES6学习



```
  babel src/index.js -o dist/index.js
 
 npm install --save-dev babel-preset-es2015 babel-cli

```



## 00.let与const

- `let`表示变量  ，`const`表示常量

- 作用域

  > 作用域在其所在的 **`{}`** 内部 ，如下代码：

  ```javascript
  if(0) {
      let test = 'hello world';
  } else {
      console.log(test)	//test is not defined
  }
  ```

- const

  > 常量（所指的地址）**不可更改**   

  ```javascript
   const age = 21; 
   age = 22 // 重新赋值会报错  Assignment to constant variable.
  ```

  > 如果 `const` 的是一个**对象**，对象所包含的值是**可以被修改**的

  ```javascript
  const Jack = {age:21}; 
  Jack.age = 22;
  console.log(Jack.age);
  ```

  

## 01.模板字符串

- **用途一**

  > 基本的字符串格式化，将表达式嵌入**字符串**中进行**拼接**。用`${}`来界定。
  >
  > **括号里面是常量的名字**  
  >
  > **注意要用反单引号 ` `` ` 将${}的内容转义**
  >
  > 如下：

  ```javascript
  //ES5 
  var name = 'xing'
  console.log('hello' + name)
  
  //ES6
  const name = 'xing'
  console.log(`hello ${name}`) //输出  hello xing
  ```

  

- **用途二**

  > 多行字符串的拼接
  >
  > - 在ES6之前我们使用`\` 来	进行多行字符串拼接
  > - ES6直接使用``` `来进行多行字符串拼接
  >
  >   **如下：**

  ```javascript
   // ES5
  var sayHello = "hello \
  world";
  console.log(sayHello)
  
  var sayHello =`hello 
  world`;
  console.log(sayHello)
  ```

  











**【参考资料】**

0.  【ES6这些就够了】https://www.jianshu.com/p/287e0bb867ae   作者：陈嘻嘻啊
1.  【[ECMAScript 6 入门】http://es6.ruanyifeng.com/#docs/intro   作者：阮一峰