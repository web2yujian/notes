# vue2 基础学习06 （Vue组件：使用组件的细节点）

### 一.使用`is`解决标签渲染中的小bug

##### 1.如下代码，将表格中的`<tr><td></td></tr>`组件化

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
    <div id="app"  >
        <table>
            <tbody>
               <row></row>
               <row></row>
               <row></row>
            </tbody>
        </table>
    </div>

    <script>
        //定义全局组件
        Vue.component('row',{
            template:`
                    <tr>
                       <td>啦啦啦</td>
                    </tr>
                    `
        }),
        new Vue({
            el:'#app'
        })

    </script>
</body>
</html>
```

**运行结果图示**

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190319220024.png)

>  乍一看是对的，但是细心的小伙伴会发现，组件row明明是引用在`tbody`中，但是在运行之后会发现:
>
> **组件解析到外面去了**  这是一个bug

##### **2.解决方法：**

> 上出现的原因是因为在`html5`中，`tbody`下必须为`tr`,如果是`row`就违背了`html5`的规范。
>
> **那么我们就这样写：**

```html
<table>
    <tbody>
        <tr is="row"></tr>
        <tr is="row"></tr>
        <tr is="row"></tr>
    </tbody>
</table>
```

**使用is**

运行结果图示：

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190319220916.png)

这时候会发现`<tr><td></td></tr>`成功解析到`tbody`中了

##### 3.其他可能会产生此bug的标签 

- select
- ul
- ol
- 等等

----------------

### 二.组件中的`data`必须为`function`形式

> 因为根节点root只会被实例一次，而组件可能会多次调用，所以要用函数返回

```javascript
 data: function(){
     return{
     	msg:'balabala'
     }
 }
```



**简写为：**

```javascript
 data(){
     return{
     	msg:'balabala'
     }
 }
```



--------------



### 三.使用`ref`操作DOM


```html
<div id="app"  >
        <div ref="hello" @click="handleClick">
               hi
        </div>
    </div>

    <script>
       
        new Vue({
            el:'#app',
            data(){
                return{
                    msg:'hello'
                }
            },
            methods:{
                handleClick(){
                    console.log(this.$refs.hello)
                }
            }
        })

    </script>
```

> 通过`this.$refs.ref的属性名`来获取dom元素
>
> 如果要获取里面的内容，则`this.$refs.ref的属性名.innerHTML`




点击之后：

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190320082936.png)





