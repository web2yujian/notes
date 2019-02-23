# Webpack 4 学习08（压缩优化css）

> 压缩css,去除注释

- 安装插件

  ```
  npm install --save-dev optimize-css-assets-webpack-plugin
  ```

- 配置`webpack.config.js`

  - 头部引入插件

    ```
    const OptimizeCssAssetsPlugin = require("optimize-css-assets-webpack-plugin") ` 
    ```

    

  | 参数                      | 意义                                                         |
  | ------------------------- | ------------------------------------------------------------ |
  | assetNameRegExp           | 正则表达式，用于匹配需要优化或者压缩的资源名。默认值是<br/>/\.css$/g |
  | cssProcessor              | 用于压缩和优化CSS 的处理器，默认是 cssnano.                  |
  | cssProcessorPluginOptions | 传递给cssProcessor的插件选项，默认为{}                       |
  | canPrint                  | 表示插件能够在console中打印信息，默认值是true                |
  | discardComments           | 去除注释                                                     |

  - 在`plugins`模块引入

  ```javascript
   new OptimizeCssAssetsPlugin({
         assetNameRegExp:/\.css$/g,
         cssProcessor:require("cssnano"),
         cssProcessorPluginOptions:{
           preset:['default',{discardComments:{removeAll:true}}]
         },
         canPrint:true
       })
  ```

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190223113520.png)



- **运行打包命令之后就可以压缩**

  `webpack --mode development`





