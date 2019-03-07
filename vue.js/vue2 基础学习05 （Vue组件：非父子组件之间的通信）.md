# vue2 基础学习05 （Vue组件：非父子组件之间的通信）

- **前言**

  > 我将要实现的是：点击按钮，将组件2中的数据传递给组件1，在组件1中展示。

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190307095300.png)

- **源代码**

  `body里面的html和js代码`

  ```html
    <div id="app">
          <component-one></component-one>
          <component-two></component-two>
      </div>
  
      <script>
          //在vue上面挂载一个$bus作为中央处理组件
          Vue.prototype.$bus = new Vue()
  
          //组件1
          var componentOne = {
              template: '<div class="componentOne">组件1 -- {{fromtwo}}</div>',
              data() {
                  return {
                      onemsg: '我是组件1的数据',
                      fromtwo: '' //接受从组件2传过来的数据
                  }
              },
              created() {
                  //1.这是方法一
                  /*var self = this //先接受 这个实例中的 this
                  this.$bus.$on('sending',function(val){
                      //this.fromtwo = val  //这里不了可以这样写，因为在这个作用域中，this代表的是 $bus中
                      self.fromtwo = val    // 这里的 
                  })*/
  
                  //2.也可以直接用箭头函数
  
                  this.$bus.$on('sending', (val) => { //箭头函数改变了this的指向
                      this.fromtwo = val
                  })
              },
          }
          //组件2
          var componentTwo = {
              template: `<div class="componentTwo">
                              组件2
                              <button @click="toOne">我要将我的数据传给组件1</button>
                          </div>`,
              data() {
                  return {
                      twomsg: '我是组件2的数据',
                  }
              },
              methods: {
                  toOne() {
                      this.$bus.$emit('sending', this.twomsg)
                  }
              },
          }
  
          new Vue({
              el: '#app',
              //声明组件
              components: {
                  'component-one': componentOne,
                  'component-two': componentTwo,
              }
          })
      </script>
  ```

  `style样式`

  ```css
   .componentOne {
          background-color: greenyellow;
          border: 1px solid green;
          width: 250px;
          height: 80px;
          margin-left: 20px
      }
  
      .componentTwo {
          background-color: lightgray;
          border: 1px solid green;
          width: 250px;
          height: 80px;
          margin-left: 20px
      }
  ```

  

- **演示**

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/GIF2.gif)





---

-  **总结步骤**

  - **创建一个空实例（bus中央事件总线也可以叫中间组件）**

  - **利用$emit  $on的触发和监听事件实现非父子组件的通信**

    ```javascript
    Vue.prototype.$bus=new Vue()//在vue上面挂载一个$bus作为中央处理组件
    this.$bus.$emit('自定义事件名','传递的数据')//触发自定义事件传递数据
    this.$bus.$on('自定义事件名'，fn)//监听自定义事件获取数据
    ```

    

>  从网上了解到，解决的方案还有`vuex`、`provide/inject`是解决同根往下派发、本地存储也可以进行非父子组件之间的通信

**这块暂时没学到，待学习。**

