# Webpack 4 学习07（提取分离打包css）

> 前面讲过 将css文件引入到js文件中，然后一起打包成js文件，现在我们学习单独提取分离css并且打包。



- 安装插件`min-css-extract-plugin`

  ```
  npm install mini-css-extract-plugin --save-dev
  ```

  

- 配置`webpack.config.js`

  - 引入插件 

    `const MiniCssPlugin =  require("mini-css-extract-plugin");`

  - rules 设置

    ```javascript
        {
          test:/\.css$/,
          use:[MiniCssPlugin.loader,'css-loader']
        }
    ```

    ​

  - plugins 设置

    ```javascript
    plugins:[
      new MiniCssPlugin({
        filename:'./css/[name].css'
      })
    ]
    ```

    **截图**

    ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190221155842.png)

- 运行命令打包