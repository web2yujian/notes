# Vue 学习基础

## 一、下载配置

#### 1.下载（前提安装了`node.js`）

```
npm install vue
```

#### 2.载完成后找到`vue.js` 放入项目文件夹

![找到文件](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225104817.png)

#### 3.放入项目文件夹

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225104943.png)



## 二、引包、留坑、实例化、插值表达式`{{}}`

#### 1.创建`html`文件进行学习

#### 2.在`html`中引入`vue.js`的包

#### 3.留坑

#### 4.实例化

#### 5.插值表达式



`上述步骤代码`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <!--2.留坑-->
  <div id="app"></div>

  <!--1.引包-->
  <script type="text/javascript" src="vue.js" ></script>

  <!--3.实例化-->
  <script>
    new Vue({
      el:'#app',
      template:`     //template里面只能有一个根节点
          <div>模板内容{{msg}}</div>
      `,
      data:function(){
        return {
          msg:'Hello Vue!'
        }
      }
    })
  </script>
</body>
</html>

```



> 注意：`template里面只能有一个根节点`



**如果有多个就会报错！！！**

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225111338.png)



## 三、常用指令

| 指令      | 用途                                                         |
| --------- | ------------------------------------------------------------ |
| v-text    | 更新元素的 textContent    (innerText)                        |
| v-html    | 更新元素的 innerHTML                                         |
| v-if      | 根据表达式的值的真假条件，销毁(remove)或重建(append)元素     |
| v-else-if | 与v-if配套使用                                               |
| v-else    | 与v-if配套使用                                               |
| v-show    | 判断是否隐藏，根据表达式之真假值，切换元素的 display CSS 属性 |
| v-for     | 循环数组、对象                                               |
|           |                                                              |

#### 1.v-text

<img src="https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225191910.png"/>

> **如果使得myText的值如下：**

```html
<div>我是text</div>
```

那么`v-text`就原样输出`<div>我是text</div>`，因为`v-text`不能解析`html`

<img src="https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225192512.png"/>



> **这时候可以用`v-html`解析**



#### 2.v-html

> 在上述情况中，将`v-text` 换成 `v-html`即可解析`html的元素`

<img src="https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225192931.png"/>



**上述代码**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <!--2.留坑-->
  <div id="app"></div>

  <!--1.引包-->
  <script type="text/javascript" src="vue.js" ></script>

  <!--3.实例化-->
  <script>
    new Vue({
      el:'#app',
      template:`     //template里面只能有一个根节点
          <div>
            <div v-text='myText'></div>
          </div>
          <!--  <div>
              <div v-html='myText'></div>
            </div>-->
      `,
      data:function(){
        return {
          myText:'<div>我是text</div>'
        }
      }
    })
  </script>
</body>
</html>

```

#### 3.v-if

<img src="https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225194404.png"/>

#### 4.v-else-if  v-else

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <!--2.留坑-->
  <div id="app"></div>

  <!--1.引包-->
  <script type="text/javascript" src="vue.js" ></script>

  <!--3.实例化-->
  <script>
    new Vue({
      el:'#app',
      template:`     //template里面只能有一个根节点
          <div>
            <div v-text='myText'></div>
            <button v-if="num==1">测试v-if</button>
            <button v-else-if="num==2">测试v-else-if</button>
            <button v-else>测试v-else</button>
          </div>

      `,
      data:function(){
        return {
          //myText:'<div>我是text</div>',
          checkvif:false,
          num:1,
        }
      }
    })
  </script>
</body>
</html>

```

![](https://github.com/HunterXing/resourse/blob/master/GIF.gif)

#### 5.v-show

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225200502.png)



#### 6.v-for

> **将数组循环出来**

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225201131.png)



```html
<ul>
    <li v-for="(item,index) in array">
        {{item}}-{{index}}
    </li>
</ul>
```

上述代码可以打印出数组的下标。

> **v-for也可以循环对象**

```javascript
<!--  <ul>
        <li v-for="obj in objs">
            {{obj}}
  	   </li>
     </ul>
  -->

<ul>
      <li v-for="(obj,key,index) in objs">
          {{key}}:{{obj}}:{{index}}
	 </li>
 </ul>

```



![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225202800.png)





## 四、vue的单、双向数据流绑定，以及事件绑定

#### 1.vue单向数据流绑定属性值  `v-bind: (属性)`   简写    ` :(属性)`

例子：`<input v-bind:value="name" v-bind:class="name">`

- 也可以绑定其他的属性，不仅仅是`value`

- 单向数据绑定 内存改变影响页面改变

- `v-bind`就是对属性的简单赋值,当内存中值改变，还是会触发重新渲染

  **下图就是绑定了value 以及 class**

  

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225205302.png)

  

#### 2.vue双向数据流 ` v-model `  只作用于有value属性的元素

例子：`<input v-model="name" v-bind:class="name">`

- 双向数据绑定  页面对于input的value改变，能影响内存中name变量
- 内存js改变name的值，会影响页面重新渲染最新值




#### 3.事件绑定`v-on:事件名="表达式||函数名"`       简写    `@事件名="表达式||函数名"`	

- 事件名可以是原生也可以是自定义的

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225211045.png)

  

#### 4.总结

v-model  双向数据绑定

- vue页面改变影响内存（js）

- 内存（js）改变影响vue页面

v-bind 单向数据绑定只是内存（js）改变影响vue页面

**源码  vue.js自行引入**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <!--2.留坑位-->
  <div id="app"></div>

  <!--1.引包-->
  <script src="./vue.js" ></script>
  <!--3.初始化-->
  <script type="text/javascript">
    new Vue({
      el:'#app',
      template:`     //template里面只能有一个根节点
          <div>
            单向数据绑定
            <input v-bind:value="name" v-bind:class="name">
            <br>双向数据绑定
            <input v-model="name" v-bind:class="name">
            <br>事件绑定
            <input type="button" v-on:click="change" value="点击我改变变量">
          </div>

      `,
      data:function(){
        return {
          name:'hello'
        }
      },
      methods:{
        change:function(){
          this.name = '🐖年好'
        }
      }
    })
  </script>
</body>
</html>
```



## 五、过滤器

> - **过滤器就是可以对我们的数据进行添油加醋然后再显示**
> - **过滤器有全局过滤器和组件内的过滤器**
>   - **全局过滤器`Vue.filter('过滤器名',过滤方式fn )`;**
>   - **组件内的过滤器 `filters:{ '过滤器名',过滤方式fn  }`**
>   - **`{{ msg | 过滤器名}}`**
> - **最终都是在过滤方式fn里面return产出最终你需要的数据**

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225212558.png)

- 组件外的过滤器

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225213739.png)

  

**注意：vue中的this是vue封装好给我们使用的，跟平常方法里面的this是不同的**



## **六、数据监听watch计算属性computed**

> #### watch监听单个，computed监听多个

思考业务场景：

1. 类似淘宝，当我输入某个人名字时，我想触发某个效果
2. 利用vue做一个简单的计算器

#### 1.watch

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <!--2.留坑-->
  <div id="app">
      <div>watch监听数据</div>
      <input type="text" v-model="msg.text">
  </div>

  <!--1.引包-->
  <script type="text/javascript" src="vue.js" ></script>

  <!--3.实例化-->
  <script>

    new Vue({
      el:'#app',
      data(){
        return{
          msg:{text:'hunter'}
        }
      },
      watch:{
      /*  msg(newval,oldval){
          console.log("新数据："+newval)
          console.log("旧数据："+oldval)
          if(newval == 'love'){
             alert('love');
          }
        }*/
        msg:{
          handler(newval,oldval){
            if(newval.text == 'love'){
               alert('love');
            }
          },
          deep:true
        }
      }
    })
  </script>
</body>
</html>

```

- **截图**

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225220119.png)



#### 当watch监听的是复杂数据类型的时候需要做深度监听（写法如下）

```javascript
watch:{
    msg:{
        handler(val){
            if(val.text=='love'){
                alert(val.text)
            }
        },
            deep:true//开启深度监听
    }
}
```

#### 2.computed

>  computed  监视对象,写在了函数内部,  凡是函数内部有this.相关属性,改变都会触发当前函数

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <!--2.留坑-->
  <div id="app">
      <div>watch监听数据</div>
      <input type="text" v-model="msg.text">
      <div>computed计算属性</div>
      <input type="text" v-model="n1">+
      <input type="text" v-model="n2">
      <input type="text" v-model="n3">={{result}}
  </div>

  <!--1.引包-->
  <script type="text/javascript" src="vue.js" ></script>

  <!--3.实例化-->
  <script>

    new Vue({
      el:'#app',
      data(){
        return{
          msg:{text:'hunter'},
          n1:'',
          n2:'',
          n3:'',
        }
      },
      watch:{
      /*  msg(newval,oldval){
          console.log("新数据："+newval)
          console.log("旧数据："+oldval)
          if(newval == 'love'){
             alert('love');
          }
        }*/
        msg:{
          handler(newval,oldval){
            if(newval.text == 'love'){
               alert('love');
            }
          },
          deep:true
        }
      },

      computed:{
        result(){
          return (Number(this.n1)+Number(this.n2))
        }
      },


    })
  </script>
</body>
</html>

```



