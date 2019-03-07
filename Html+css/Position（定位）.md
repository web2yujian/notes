# Position（定位）

>  **position可以取五个值**

| 参数     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| absolute | **绝对定位**；脱离⽂档流的布局，遗留下来的空间由后⾯的元素填充。定位的起始位置为最近的⽗元素(postion不为static)，否则为Body⽂档本身。 |
| relative | **相对定位**；不脱离⽂档流的布局，只改变⾃身的位置，在⽂档流原先的位置遗留空⽩区域。定位的起始位置为此元素原先在⽂档流的位置。 |
| fixed    | **固定定位**；类似于absolute，但不随着滚动条的移动⽽改变位置。 |
| static   | **默认值；默认布局。** **忽略 top, bottom, left, right和z-index** |
| inherit  | **从父元素继承**该属性的值                                   |



以上的`absolute` 和`fixed` 可以使得元素脱离文档流。

position属性只是定义元素的定位方式，要想此元素能按照希望的位置显示，就需要使⽤下⾯的属性(**position:static不⽀持这些**)：

- **left** ： 表示向元素的左边插⼊多少像素，使元素向右移动多少像素。

- **right** ：表示向元素的右边插⼊多少像素，使元素向左移动多少像
  素。

- **top** ：表示向元素的上⽅插⼊多少像素，使元素向下移动多少像素。

- **bottom** ：表示向元素的下⽅插⼊多少像素，使元素向上移动多少像
  素。

  >  上⾯属性的值可以为负，单位：**px** 。

--------------------------



### 绝对定位(absolute)

> 脱离⽂档流的布局，遗留下来的空间由后⾯的元素填充。
>
> 定位的起始位置为**最近的⽗元素**(postion不为static)，否则为Body⽂档
> 本身。

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228211747.png)



-----------------------------------





### 相对定位(relative)

> 不脱离⽂档流的布局，只改变⾃身的位置，在⽂档流原先的位置遗留空⽩区域。
>
> 定位的起始位置为**此元素原先在⽂档流的位置**。



![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228212023.png)

--------------------------



### 固定定位(fix)

>  类似于absolute，但不随着滚动条的移动⽽改变位置。

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228212145.png)

-------------------



### 默认定位(static)

>  表示此元素为默认定位⽅式。

--------------



### 继承(inherit)

>  从父元素继承定位⽅式。

**1.父容器的`position`属性为`relative`**



![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190302151946.png)

由上图可知，div继承了父类的position属性（relative）;这时候div-a没有脱离文档流，只是相对于原来的位置向右边偏移了，留下一个空位。参考绝对定位的图形。



**注意：此时的父容器是没有设置宽高的，（见图）**，我们可以看见**父容器宽度为100%，高度自适应。**



下面我们把父容器的定位改成`absolute	`

**2.父容器的`position`属性为`absolute`**

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190302152959.png)



可以看出，div-a脱离了文档流，相对于父容器向右偏移了350px，后面的div-b占据了他的位置.



**注意：此时我们可以发现，父容器宽和高都是自适应的。**

------



然后我们在对两种情况进行研究。

1. 父容器postion属性为`static`

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190302153811.png)

   **父容器宽度为100%，高度自适应。**

   

2. 父容器的position属性为`fixed`

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190302154043.png)

   **父容器宽高均自适应**

--------------------



从这里面。我们不仅可以看出`inherit`的特性。而且我们还发现了以下规则：

**重点**

在父容器没有设置宽高的时候，

- 当父容器定位为`relative`和`static`时，及没有脱离文档流时，宽度为100%
- 当父容器定位为`absolute`和`fixed`时，及脱离文档流时，宽高为自适应




