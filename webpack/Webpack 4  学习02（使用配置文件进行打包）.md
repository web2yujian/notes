# Webpack 4  学习02（使用配置文件进行打包）

> 上一讲中我们打包没有用到`webpack.config.js`配置文件，webpack4把自己定位为一个零配置的工具。这一讲学习配置文件使用，更好地学习webpack。

[上一讲 Webpack 4  学习01（基础配置）](https://www.jianshu.com/p/5b849114fe89)



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

