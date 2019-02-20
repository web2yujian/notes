# Webpack 4  学习笔记

## 一、安装配置

- 【**前提**】安装`node.js`环境

  【官网下载】https://nodejs.org/zh-cn/

  > 安装教程不赘述

- 创建项目文件夹

  例如创建如下文件夹`webpack_demo1`

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220193717.png)

- 创建配置项

  ```
  npm init -y
  ```

  生成一个`package.json`文件  如下图

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220194000.png)

  

- 全局安装`webpack` **（不推荐，进行下一步操作）**

  ```
  npm install webpack -g
  ```

- 局部安装`webpack`**(推荐)** 

  ```
  npm install webpack --save-dev
  ```

  - 另外，`webpack 4`要求安装包

  ```
  npm install webpack-cli --save-dev
  ```

  一起安装

  ```
  npm install webpack webpack-cli --save-dev
  ```

  **以下表示安装成功**

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220194403.png)		

- 创建入口文件

  ```
  ./src/index.js
  ```

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220194642.png)

  任意编写`index.js`文件内容用于测试



- 配置生产和开发模式

  打开`package.json`文件添加如下脚本

  ```
  "scripts": {
    "dev": "webpack --mode development",
    "build": "webpack --mode production"
  }
  ```

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220195105.png)

- 现在运行：

  ```
  npm run dev
  ```

  生成`dist/main.js` ，其中 `main.js` 没有压缩 

  > `npm run dev` 表示**开发模式**

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220195447.png)

  

  ```
  npm run build
  ```

  此时的`main.js` 被压缩 ，这便是**生产模式**

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220200028.png)



- 接下来看看打包的js文件是否能够使用

  - 创建`index.html` 引入打包好的`main.js`

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="./main.js" charset="utf-8"></script>
  </head>
  <body>
  
  </body>
  </html>
  ```

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220200402.png)

  - 打开浏览器调试

    ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220200725.png)

​	

​	**输出结果表示打包成功，大功告成 ！！！**



​		

​	

​	

​		







