# Webpack 4 学习09（打包生成html）

> 所需插件  `html-webpack-plugin`   本教程基于已经搭建好的webpack环境，详见[ Webpack 4  学习01（基础配置）](https://www.jianshu.com/p/5b849114fe89)

- **了解`html-webpack-plugin**`

  > HtmlWebpackPlugin会自动为你生成一个HTML文件，根据指定的index.html模板生成对应的 html 文件。

- **安装依赖**

  ```powershell
  npm install html-webpack-plugin --save-dev
  ```

- **配置`webpack.config.js`文件**

  - 在头部定义常量，引入插件

    ```javascript
    const HtmlWebpackPlugin = require('html-webpack-plugin')
    
    ```

   - **在`plugins`模块引入**

     ```javascript
     new HtmlWebpackPlugin({
            template:'./public/index.html',  //模板文件路径
            filename:'webpack.html',         //生成的html文件名称
            minify:{
              minimize:true,                 //打包为最小值
              removeAttributeQuotes:true,    //去除引号
              removeComments:true,           //去除注释
              collapseWhitespace:true,       //去除空格
              minifyCSS:true,                //压缩html内css
              minifyJS:true,                 //压缩html内js
              removeEmptyElements:true,      //清除内存为空的元素
            },
            hash:true                        //引入产出资源的时候加上哈希避免缓存
          })
     ```

     



- **运行打包命令之后就可以压缩**

  `webpack --mode development`

- **打包效果**

  > public 下的 index.html 打包成为 build下面的 webpack.html啦。

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190223123214.png)