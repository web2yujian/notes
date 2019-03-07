# vue2 基础学习02 （Vue组件）



[vue学习路径和建议----尤雨溪](https://zhuanlan.zhihu.com/p/23134551)
	
[vue官网](https://cn.vuejs.org/v2/guide/)

### 1.Vue组件

**参考官方文档：**[组件基础](https://cn.vuejs.org/v2/guide/components.html)

1. 定义一个组件

   ```javascript
   // 定义一个名为 button-counter 的新组件
   Vue.component('button-counter', {
     data: function () {
       return {
         count: 0
       }
     },
     template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
   })
   ```

   上面的`button-counter`就是一个组件，可以说是一个**自定义的标签**，我先这样理解，后面再看。

   > **注意！！！**

   - **一个组件的 data 选项必须是一个函数**

     ```javascript
     data: function () {
       return {
         count: 0
       }
     }
     ```

   - **template下面只能有一个根节点**

     如果再创建一个同级的节点就会出错，如下：

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190304192815.png)

2. 在html中引用这个组件

   ```html
   <div id="components-demo">
     <button-counter></button-counter>
   </div>
   ```

   

3. 实例化Vue  **（指向组件所在的"坑位"）**

   ```javaScript
   new Vue({ el: '#components-demo' })
   ```

   

4. 可以复用

   ```html
   <div id="components-demo">
     <button-counter></button-counter>
     <button-counter></button-counter>
     <button-counter></button-counter>
   </div>
   ```





  
