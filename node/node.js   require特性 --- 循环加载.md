#  node.js   require特性 --- 循环加载

> #### 一旦出现某个模块被循环加载，就只输出已经执行的部分，还未执行的部分不会输出

----------



`moduleA.js`

```javascript
// 暴露外部可引用的变量 testValA
let textValA = 'A'
module.exports.textValA = textValA;
// 引入模块B
const mB = require ('./moduleB');
console.log(`mA执行： ${mB.textValB}`);

// 重写模块A中的变量testvalA
module.exports.textValA = 'AA';

```

`moduleB.js`

```javascript
// 暴露外部可引用的变量 testValB
let textValB = 'B'
module.exports.textValB = textValB;
// 引入模块B
const mA = require ('./moduleA');
console.log(`mB执行： ${mA.textValA}`);

// 重写模块A中的变量testvalB
module.exports.textVal = 'BB';

```

`main.js`

```javascript
require ('./moduleA');
require ('./moduleB');
```



`terminal运行：`

> 执行：`node moduleB.js`

```
mA执行： B
mB执行： AA
```

