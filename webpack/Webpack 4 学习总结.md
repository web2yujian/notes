# Webpack 4 学习总结

## 一、安装配置

- 【**前提**】安装`node.js`环境

  【官网下载】https://nodejs.org/zh-cn/
   **安装教程不赘述**

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

  

  **输出结果表示打包成功，大功告成 ！！！**



## 二、使用配置文件进行打包

> 上一讲中我们打包没有用到`webpack.config.js`配置文件，webpack4把自己定位为一个零配置的工具。这一讲学习配置文件使用，更好地学习webpack。



- 根目录下新建一个`webpack.config.js`文件 （记载配置信息）

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220205200.png)

  

- 配置文件

  ```javascript
   const path = require('path');
  
   module.exports = {
     entry:'./public/index.js',
     output:{
       path:path.resolve(__dirname,'build'),
       filename:'bundle.js'
     }
   }
  ```

  

  | 字段         | 意义                                   |
  | ------------ | -------------------------------------- |
  | entry        | 入口，所需打包的文件的路径             |
  | output       | 出口                                   |
  | path         | 文件打包后存放的路径                   |
  | path.solve() | 将路径或者路径片段的序列处理成绝对路径 |
  | _dirname     | 表示当前文件所在目录的绝对路径         |
  | filename     | 打包后文件的名称                       |

  

- 按照配置项新建一个入口文件`public/index.js`

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190220210554.png)

- 运行`npm run dev`





## 三、配置入口和出口的进阶使用

### 一、单出口形式

`webpack.config.js`

```javascript
const path = require('path');


module.exports = {
  //单出口形式
  entry:['./public/index.js','./public/index2.js'],//有多个文件
  output:{
    path:path.resolve(__dirname,'build'),
    filename:'bundle.js'
  }
}
```



![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190221084217.png)



- 运行`npm run dev`   

  > 生成唯一的打包文件 `bundle.js`

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190221084406.png)



### 二、多出口形式

	`webpack.config.js`

```json
const path = require('path');

module.exports = {
  //多出口形式
  entry:{
    entryOne:'./public/entryOne/index.js',
    entryTwo:'./public/entryTwo/index.js',
  },
  output:{
    path:path.resolve(__dirname,'build'),
    filename:'[name].js'
  }
}
```

​	

- 文件结构

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190221084849.png)

  

- 运行`npm run dev`   

  - 生成两个打包文件

    ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190221085037.png)



## 四、配置webpack-dev-server

### 一、了解 webpack-dev-server

- `webpack-dev-server`用来配置本地服务器
- 为 `webpack` 打包生成的文件提供web服务
- 自动刷新和热替换（HMR）



### 二、安装webpack-dev-server

``` 
npm install --save-dev webpack-dev-server
```





### 三、 配置webpack.config.js文件

 

```javascript
devServer:{
		contentBase:'./dist',  //设置服务器访问的基本目录
		host:'localhost', //服务器的ip地址
		port:8080,  //端口
		open:true  //自动打开页面
}
```

 

### 四、配置package.json



```json
"scripts": {
    "start": "webpack-dev-server --mode development"
 }
```





### 五、运行命令

`npm run dev` 打包文件

`npm run start `打开服务器





--------------------

## 五、打包css

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

    

  ------------

  

  

  

## 六、使用babel编译ES6

- **babel转化语法所需依赖项**：

  - `babel-loader`： 负责 `es6 `语法转化
  - `babel-core`： `babel`核心包
  - `babel-preset-env`：告诉`babel`使用哪种转码规则进行文件处理

- **安装依赖**

  ```
  npm install babel-loader @babel/core @babel/preset-env --save-dev
  ```

- **配置`webpack.config.js`文件**

  ```javascript
    	{
        test:/\.js$/,
        exclude:/node_modules/,
        use:'babel-loader'
      }
  ```

  

- **新建 `.babelrc `文件配置转换规则**

  ```
  {
    "presets":["@babel/preset-env"]
  }
  ```

  

- 或者直接在`webpack.config.js`文件中配置规则

  ```javascript
    	{
        test:/\.js$/,
        exclude:/node_modules/,
        use:{
        	loader:'babel-loader',
        	options:{
              presets:['@babel/preset-env']
        	}
        }
      }
  ```

  ----------------

  ## 	


## 七、提取分离打包css

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

    

  - plugins 设置

    ```javascript
      new MiniCssPlugin({
        filename:'./css/[name].css'
      })
    
    ```

    **截图**

    ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190221155842.png)

- 运行命令打包

--------------



## 八、压缩优化css

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