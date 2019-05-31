# vue 中使用 vue-echarts 插件

## 安装依赖

```markdown
npm install vue-echarts --save
```

## 引入依赖

`main.js`

```javascript
import ECharts from 'vue-echarts/components/ECharts'

Vue.component('chart', ECharts)
```



## 在组件中使用echarts

> 首先得在`Script`中引入需要的图表类型和参数组件

```javascript
<script>
    // 折线
    import 'echarts/lib/chart/line'
    // 饼状图
    import 'echarts/lib/chart/pie'
    // 柱状图
    import 'echarts/lib/chart/bar'
    // ...

    // 提示
    import 'echarts/lib/component/tooltip'
    // 图例
    import 'echarts/lib/component/legend'
    // 标题
    import 'echarts/lib/component/title'
    // ...
    export default {
        // ...
    }
</script>
```

> 然后就可以在`<template>`中使用

```html
<template>
    <div>
        <chart  :options="options" :auto-resize="true"></chart>
    </div>
</template>
```

> 定义动态的options参数 **引号中参数可以换其他的名称**

```javascript
data () {
    return {
        options: {}
    }
}
```

> 在页面挂载时赋值获取的options   // 注意**这里可以是从后台获取的**，现在我们用数据模拟

```javascript
mounted () {
    this.option = {
        // 标题
         title: {
          text: '某某图'
          x: 'center',
          textStyle: {
            color: '#fff',
            fontSize: 18,
            fontWeight: 'normal'
          }
        },
        // 工具提示
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b} : {c} ({d}%)'
        },
        // 图例说明
        legend: {
          show: true,
          x: 'center',
          bottom: 20,
          data: ['直接访问','邮件营销','联盟广告','视频广告','搜索引擎'],
          textStyle: {
            color: '#fff',
            fontSize: 20
          }
        },
        // 各个部分的颜色
        color: ['#18DBDF', '#F6EF7B', '#3DE16F', '#EF69FB', '#FE5679'],
        // 拖拽的时候重新渲染  默认关闭
        calculable: true,
        // 工具箱
        toolbox: {	
            show : true,
            feature : {
                mark : {show: true},
                dataView : {show: true, readOnly: false},
                magicType : {
                    show: true,
                    type: ['pie', 'funnel'],
                    option: {
                        funnel: {
                            x: '25%',
                            width: '50%',
                            funnelAlign: 'left',
                            max: 1548
                        }
                    }
                },
                restore : {show: true},
                saveAsImage : {show: true}
            }
        },
        label: {
          show: true,
          fontSize: 20
        },
        series : [
            {
                itemStyle: {
                  normal: {
                    label: {
                      show: true,
                      formatter: '{b} : {c} ({d}%)'
                    },
                    labelLine: {
                      show: true
                    }
                  }
                },
                name:'访问来源',
                // 类型：这里是饼图
                type:'pie',
                radius : '55%',
                center: ['50%', '60%'],
                // 数据
                data:[
                    {value:335, name:'直接访问'},
                    {value:310, name:'邮件营销'},
                    {value:234, name:'联盟广告'},
                    {value:135, name:'视频广告'},
                    {value:1548, name:'搜索引擎'}
                ]
            }
        ]
    }
}
```

