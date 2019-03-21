# vue2 基础学习07（组件参数校验）



> 父组件向子组件传递参数，子组件有权对这些参数进行约束，这些约束就可以叫做**组件参数校验**

##### 源码：

```html
<div id="app"  >
        <child :content="content"></child>
    </div>

    <script>
       
        Vue.component('child',{
            props:{
                content:{
                    type:String,                 //表示content必须为String类型
                    required:true,                //表示属性必传，  false为反
                    default:'Default Value' ,     //表示属性的默认值 ，（当required为false,content没有的时候）
                    validator:function(value){    //更复杂的自定义校验器
                        return (value.length > 5)
                    }
                }
            },
            template:`<div>{{content}}</div>`
        }),
        new Vue({
            el:'#app',
            data(){
                return{
                    content:'hello'
                }
            }
        })

    </script>
```

##### 

