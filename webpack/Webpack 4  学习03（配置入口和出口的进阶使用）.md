

# Webpack 4  学习03（配置入口和出口的进阶使用）

## 一、单出口形式

`webpack.config.js`

```
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



## 二、多出口形式

​	`webpack.config.js`

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