# Webpack 4 学习10 (运用webpack插件拷贝静态文件(copy-webpack-plugin))

- 安装插件

  ```
  npm install --save-dev copy-webpack-plugin
  ```

  

- 配置`webpack.config.js`

  - 头部引入插件

    ```javascript
    const CopyWebpackPlugin = require('copy-webpack-plugin');
    ```

    

  - 在`plugins`模块引入

    ```javascript
     new CopyWebpackPlugin([
           {
             from:__dirname+'/public/lib',
             to:__dirname+'/build/lib'
           }
         ])
    ```

    


- **运行打包命令**

  `webpack --mode development`

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190223132404.png)