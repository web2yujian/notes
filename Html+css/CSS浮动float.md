# CSS浮动float

参考教程（[经验分享：CSS浮动(float,clear)通俗讲解](https://www.cnblogs.com/iyangyuan/archive/2013/03/27/2983813.html)）

首先了解一下标准文档流的排版：**从上到下，从左到右，遇块换行**

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228142910.png)

----------------

浮动可以理解为让某个div元素脱离文档流，漂浮在文档流之上

#### block元素无视float元素

啥意思呢，就是A和B两个block(块级)元素在排队买东西，A在前面，那么B只能遵守规则（标准文档流的遇块换行）突然A膨胀了，飘了，然后B就无视A,前进一步跑到A下面。

下图就是这种情况。

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228145646.png)



​	but，如果此时A没有浮动，而**B浮动**了，此时他只漂浮在自己的位置上方。从俯视图看似乎没有脱离文档流。

​	![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228151737.png)

#### inline元素像流水一样围绕着float元素

行内元素会围绕着浮动的元素进行排列

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228150029.png)

#### 清除浮动可以理解为打破横向排列。

​      语法：

​       `clear : none | left | right | both`

​       取值：

​      ` none ` :  默认值。允许两边都可以有浮动对象

​      ` left`   :  不允许左边有浮动对象

​     `  right`  :  不允许右边有浮动对象

​      ` both ` :  不允许有浮动对象

 

例子：

假如页面中只有两个元素div1、div2，它们都是左浮动，场景如下：

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228153514.png)



如果想要清除浮动，很多人在`div1`的CSS样式中添加`clear:right`;然而这样子是没有用的。

  **对于CSS的清除浮动(clear)，一定要牢记：这个规则只能影响使用清除的元素本身，不能影响其他元素。**

所以在`div2`中CSS样式中添加`clear:left`;`

