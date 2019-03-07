# vue组件之组件间的通信

#### 一、父子组件间的通信

- 一个简单的例子

  > 如图，下面有个目录结构：父组件下面有个子组件。
  >
  > 我们要实现的就是：
  >
  > - 子组件接受父组件的data数据
  > - 点击子组件中按钮，可以将子组件中数据反馈给父组件

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190306203946.png)

  **直接上代码：**

  ```html
  <div id="app"></div>
     
      <script>
          //子组件
          var child = {
              template: `
          <div class="child">
              子组件---> {{fromfather}}   <br > 
              <button @click='sendParent'>反馈信息给父组件</button>
          </div>
        `,
              props: ['fromfather'],
              data(){
                  return{
                      childmsg:'我是子组件的数据'
                  }
              },
              methods: {
                  sendParent() {
                      this.$emit('fromchild', this.childmsg)
                  }
              }
          }
  
          // 父组件
          var parent = {
              template: `<section>
                              父组件 ----> {{fromchildmsg}}
                              <child v-bind:fromfather="msg" @fromchild='getdata'></child>
                        </section>
          `,
              //声明子组件
              components: {
                  child
              },
              //父组件的数据，准备让子组件接受
              data() {
                  return {
                      msg: '我是父组件的数据',
                      fromchildmsg:''
                  }
              },
              methods: {
                  getdata(val) {
                      this.fromchildmsg = val
                  }
              }
          }
  
          new Vue({
              el: '#app',
              components: {
                  parent
              },
              template: `
                  <div>
                      <parent class="parent"></parent>
                  </div>
        `
          })
  
      </script>
  
  ```

  **点击后效果如图：**

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190306205013.png)

  > 箭头后面的即是从其他组件中传过来的数据

#### 二、非父子组件间的通信

#### 三、总结

- **父传子**

  - 父用子的时候通过**属性传递**
  - 子要声明`props:['属性名'] `来接收
  - 收到就是自己的了，随便你用
    - 在template中 直接用
    - 在js中 this.属性名 用

- **子传父**

  - 子组件里通过`$emit('自定义事件名',变量1，变量2)`触发

  - 父组件`@自定义事件名=‘事件名’`监听

  - 如：

    ```html
    子组件方法里 this.$emit('sendfather',val1,val2)触发自定义事件
    父组件里  <child @sendfather='mymethods'></child>
    ```

    