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

```javascript
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

| 指令      | 用途           |
| --------- | -------------- |
| v-text    | 赋值innerText, |
| v-html    |                |
| v-if      |                |
| v-else-if |                |
| v-else    |                |
| v-show    |                |
| v-for     |                |
|           |                |



## 一、引包
## 一、引包
## 一、引包
## 一、引包
## 引包
## 一、引包
## 一、引包
## 一、引包
## 一、引包
## 一、引包
## 一、引包
## 一、引包
## 一、引包



