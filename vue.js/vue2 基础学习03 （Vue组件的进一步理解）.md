# vue2 基础学习03 （Vue组件的进一步理解）



[vue学习路径和建议----尤雨溪](https://zhuanlan.zhihu.com/p/23134551)
	
[vue官网](https://cn.vuejs.org/v2/guide/)

>  今天看了慕课网的一个教学视频   [Vue入门](https://www.imooc.com/learn/980)  感觉清晰了很多



#### 首先引入一个简单的todolist案例

- **初始化项目（引入`vue.js`部分省略）**

  ```html
   <!-- 挂载点 -->
      <div id="app"> 
          
      </div>
  
      <script>
          var app = new Vue({
              el: '#app', //通过id选择器挂载上去 
          })
      </script>
  ```

  

- **初始化数据，遍历输出**

  ```html
  <!-- 挂载点 -->
      <div id="app"> 
          <!--  -->
          <div>
              <input type="text" >
              <button>添加任务</button>
  
              <ul >
                  <li v-for="(item, index) in list" :key="index">{{item}}</li>
              </ul>
          </div>
         
      </div>
  
      <script>
          var app = new Vue({
              el: '#app', //通过id选择器挂载上去 
              data(){     //介意这样写data，因为在后面的vue-cli里面就是这样写的 自我理解
                  return{
                      list:[1,2,3]   // 先把写死后面再更改
                  }
              }
          })
      </script>
  ```

  **以下是效果：**

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190305153038.png)

-  **接下来就是动态添加数据了**

  ```html
     <!-- 挂载点 -->
      <div id="app"> 
          <!--  -->
          <div>
              <input type="text" v-model="listValue">
              <button v-on:click="addList">添加任务</button>
  
              <ul >
                  <li v-for="(item, index) in list" :key="index">{{item}}</li>
              </ul>
          </div>
         
      </div>
  
      <script>
          var app = new Vue({
              el: '#app', //通过id选择器挂载上去 
              data(){     //介意这样写data，因为在后面的vue-cli里面就是这样写的 自我理解
                  return{
                      list:[],   // 先把写死后面再更改，
                      listValue:'' // 把这个值双向绑定在 input中
                  }
              },
              methods: {
                  addList:function(){
                      this.list.push(this.listValue)   //往数组中push数据，数据来源是input中的值
                      this.listValue = ''             //添加完之后记得将input中间数据清空
                  }
              }
          })
      </script>
  ```

  > 以上涉及数据的双向绑定

  



#### 以下是将todolist应用进行了组件化

- 对todolist组件进行拆分。

  ```htmL
  <div id="app">
          <div>
              <input v-model="inputValue">
              <button @click="handleSubmit">提交</button>
          </div>
          <ul>
       
              <todo-item 
                  v-for="(item, index) in list" 
                  :key="index" 
                  :content="item" 
                  :index="index"
                  @delete='handleDelete'
              >
              </todo-item>
          </ul>
      </div>
  
      <script>
          //全局组件 
          Vue.component('todo-item', {
              props:['content','index'],//相当于接收父节点的属性
              template: ` <li v-on:click="handleClick">{{content}}{{index}}</li>`
              ,
              methods:{
                  handleClick:function(){
                      this.$emit('delete',this.index)//相当于传递给父类
                  }
              }
          })
  
  
          // //局部组件
          // var toDoItem = {
          //     template: `<li >item</li>`
          // }
  
          var app = new Vue({
              el: '#app',
             
              //局部组件的声明
              // components: {
              //     'todo-item': toDoItem
              // },
              data: {
                  inputValue: '',
                  list: []
              },
              methods: {
                  handleSubmit: function () {
                      this.list.push(this.inputValue)
                      this.inputValue = ""
                  },
                  handleDelete: function(index){
                     this.list.splice(index,1)
                  }
              }
          })
  ```



***总结：***

- 子组件向父组件传递参数：  通过绑定属性的形式

- 父组件向子组件： 发布订阅模式