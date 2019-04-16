# 使用Vuex实现数据共享

#### 初步理解

![图片来自官网](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190413211348.png)



> Vuex 可以帮助我们管理**共享状态** 

- State: 所有的公用**数据**都存放在State之中，如果组件想用公用数据，直接去调用即可。（后面说明）
- Actions：改变State中数据的**操作**（异步操作或者复杂的同步操作）放在其中  （有时候可以略过）
- Mutations: 放置同步的对State的修改  （必须经过Mutations）

步骤：调用Action，再调用Mutations，最后更改State中数据，数据发生变化时，组件上数据就会发生变化 。

#### 在脚手架工具中的使用

##### 1.安装

```javascript
npm install vuex --save
```

##### 2.引入 （此部分代码在下方第3步的`index.js`中引入）

```
import Vuex from 'vuex'

Vue.use(Vuex)
```

#### 3.在`src`目录下创建`store`

![目录结构](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190413213209.png)

