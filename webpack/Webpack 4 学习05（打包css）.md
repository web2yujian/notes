# Webpack 4 学习05（打包css）

> webpack 自身只理解 JavaScript， 想让 webpack 能够去处理那些非 JavaScript 文件，我们将使用到`loader`
>
> loader 可以将所有类型的文件转换为 webpack 能够处理的有效模块，然后你就可以利用 webpack 的打包能力，对它们进行处理。



- **安装loader**

    `npm install style-loader css-loader --save-dev`

- **配置loader**

  - 在`webpack.config.js`文件里配置module中的rules，如下：

    -  test 属性，用于标识出应该被对应的 loader 进行转换的某个或某些文件。
    -  use 属性，表示进行转换时，应该使用哪个 loader。

    ```javascript
    module.exports = {
        /*入口和出口文件可以不用配置，默认*/
    
        module:{
          rules:[
            {
              test:/\.css$/,
              use:['style-loader','css-loader']//引入的顺序至关重要,不可改变
            }
          ]
        }
    }
    ```

    

- **测试是否打包成功**

  - 在`src`下创建`index.css`文件

    ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190221132534.png)

  - 在`index.js`中引入`index.css`文件

    `require('!style-loader!css-loader!./index.css');`

    ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190221132749.png)

    

  - 进行打包后运行 `npm run dev`（之前配置好，详见[第一篇文章：webpack4 基础配置](https://www.jianshu.com/p/5b849114fe89)）

    红色的背景，控制台输出`hello`

    ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190221133106.png)

    

  