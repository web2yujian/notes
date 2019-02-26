# vue组件化开发

### 一、组件化开发

#### 1.创建组件的两种方式

```javascript
  var Header = {
  	template:'模板' ,
      data是一个函数,
      methods:功能,
      components:子组件们 
  }//局部声明
```

  


  ```javascript
  Vue.component('组件名',组件对象);//全局注册 等于注册加声明了
  ```



#### 2.组件类型

- 通用组件（例如表单、弹窗、布局类等)
- 业务组件（抽奖、机器分类）
- 页面组件（单页面开发程序的每个页面的都是一个组件、只完成功能、不复用）

#### 3.组件开发三步曲：声明、注册、使用



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

  // 局部创建
    var myHeader =Vue.extend(
      {
        template:`
            <header>头部</header>
        `
      }
    )
    // 语法糖形式的局部创建
    var myContent ={
        template:
        `<section>内容</section>`
    }
  //全局创建   不用在下面的components中声明
    Vue.component('myFooter',{
      template:
      `
        <footer>我是尾部</footer>
      `
    }),
    new Vue({
      el:'#app',
      components:{
        myHeader,
        myContent
      },
      template:`
          <div>
            <my-header></my-header>
            <my-content></my-content>
            <my-footer></my-footer>
          </div>
      `,
      data:function(){
        return {
            
        }
      }
    })
  </script>
</body>
</html>

```





### 二、slot插槽和ref、$parent

#### 1.slot插槽

- ##### slot就是子组件里给DOM留下的坑位

- ##### <子组件>DOM</子组件>

- ##### slot是动态的DOM

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


    // 语法糖形式的局部创建
    var parent ={
        template:
        `<section>
          内容
          <slot name="slot1"></slot>
        </section>`
    }
    var child ={
      template:
      `
        <div>我是插槽内容</div>
      `
    }

    new Vue({
      el:'#app',
      components:{
        parent,
        child
      },

      template:`
          <div>
            <parent>
              <child slot="slot1"></child>
            </parent>
          </div>
      `,

    })
  </script>
</body>
</html>

```



​	

#### 2.ref获取子组件实例

- ##### 识别：在子组件或元素上使用属性ref="xxxx"

- ##### 获取：this.$refs.xxxx 获取元素

- ##### $el 是拿其DOM

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


    // 语法糖形式的局部创建
    var parent ={
        template:
        `<section>
          内容
          <slot></slot>
        </section>`
    }
    var child ={
      template:
      `
        <div>我是插槽内容</div>
      `
    }

    new Vue({
      el:'#app',
      components:{
        parent,
        child
      },

      template:`
          <div>
            <parent>
              <child ref="childs"></child>
            </parent>
          </div>
      `,
      mounted(){
        console.log(this.$refs.childs)
      }
    })
  </script>
</body>
</html>

```



#### 3.$parent获取父组件实例（可在子组件直接使用this.$parent即可）





### 三、父子组件的通信



#### 1.父传子

- 父用子的时候通过属性传递
- 子要声明`props:['属性名']` 来接收
- 收到就是自己的了，随便你用
  - 在`template`中 直接用
  - 在js中 `this.属性名` 用

#### 2.子传父

- 子组件里通过`$emit('自定义事件名',变量1，变量2)`触发
- 父组件`@自定义事件名=‘事件名’`监听

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

    var child ={
      template:
      `
        <div>
        子组件-{{sendChild}}
        <button @click='sendParent'>我要反馈东西给父亲</button>
        </div>
      `,
      props:['sendChild'],
      methods:{
        sendParent(){
          this.$emit('baba','这是儿子组件给你的')
        }
      }
    }
    // 语法糖形式的局部创建
    var parent ={
        template:
        `<section>
             父组件---{{msg}}
             <child sendChild="父亲给你的" @baba='reserve'></child>
        </section>`
      ,
      components:{
        child
      },
      data(){
        return{
          msg:''
        }
      },
      methods:{
        reserve(val){
          this.msg=val
        }
      }
    }

    new Vue({
      el:'#app',
      components:{
        parent
      },
      template:`
        <div>
          <parent></parent>
        </div>
      `
    })
  </script>
</body>
</html>

```



### 四、非父子组件之间的通信

