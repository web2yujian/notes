# Webpack 4 学习11（用clean-webpack-plugin来清除文件）

> 当我们修改带hash的文件并进行打包时，每打包一次就会生成一个新的文件，而旧的文件并没有删除。为了解决这种情况，我们可以使用`clean-webpack-plugin`在打包之前将文件先清除，之后再打包出最新的文件

- 下载插件依赖

  ```
  npm install --save-dev clean-webpack-plugin
  ```

- 配置`webpack.config.js`

  - 头部引入插件

    ```javascript
    const CleanWebpackPlugin = require('clean-webpack-plugin');
    ```

    

  - 在`plugins`模块引入

    ```javascript
     new CleanWebpackPlugin(['build'])
    ```

    


- **运行打包命令**

  `webpack --mode development`

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190223132404.png)

