

jQuery对象和DOM对象

##  一 、顶级对象

1. #### 浏览器中的顶级对象

   > window

2. #### 页面中的顶级对象

   > document

3. #### jQuery中的顶级对象

   > $   或者 jQuery  

   - 用法：`$.方法();`或者`$.属性`
   - `$`可以用`jQuery`代替

## 二、区别

> **通过一个例子**

```html
<input type="button" value="按钮" id="btn">
```

- 以上的按钮如果通过DOM获取就是**DOM对象**；

  ```javascript
  var btnObj1 = document.getElementById('btn');
  ```

- 以上的按钮如果通过`$`或者`jQuery`获取就是**jQuery对象；**

  ```javascript
  var btnObj2 = $('#btn');
  ```

> **注意**：`btnObj1`和`btnObj2`**不是一个对象**。如下图：在**Chrome调试工具Developer Tools**调试，判断，返回为`false`。即两者不是一个对象

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20180923220924.png)

- 另外，**为了代码更具可读性**。可以预先约定的一种命名格式，对于jQuery对象命名可以为一下格式（非强制）：(`$btnObj2`的`$`在这里就是变量中的一个字母，跟`_btnObj2`一个道理。)



```javascript
var $btnObj2 = $('#btn');
```

- 如下：

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20180923224201.png)

##  三、jQuery对象和DOM对象之间的转换

> ### jQuery对象和DOM对象不能使用对方的方法，如果要强行使用，则必须的转换成对方的类型

 ###  1.jQuery对象转换为DOM对象

- 直接在后面加上`[0]`

```javascript
btnObj2[0]
```

### 2.jQuery对象转换为DOM对象

- 用`$`包裹

  ```javascript
  $(btnObj1)
  ```



  -  **通过下图可以看出:**

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20180924094107.png)

