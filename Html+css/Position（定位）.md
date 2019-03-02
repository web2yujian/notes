# Position（定位）

> **①absolute ：**绝对定位；脱离⽂档流的布局，遗留下来的空间由后⾯的元素填充。定位的起始位置为最近的⽗元素(postion不为static)，否则为Body⽂档本身。
> **②relative ：**相对定位；不脱离⽂档流的布局，只改变⾃身的位置，在⽂档流原先的位置遗留空⽩区域。定位的起始位置为此元素原先在⽂档流的位置。
> **③fixed ：**固定定位；类似于absolute，但不随着滚动条的移动⽽改变位置。
> **④static ：**默认值；默认布局。



以上的`absolute` 和`fixed` 可以使得文档脱离文档流。

position属性只是使元素脱离⽂档流，要想此元素能按照希望的位置显示，就需要使⽤下⾯的属性(**position:static不⽀持这些**)：

- **left** ： 表示向元素的左边插⼊多少像素，使元素向右移动多少像素。

- **right** ：表示向元素的右边插⼊多少像素，使元素向左移动多少像
  素。

- **top** ：表示向元素的上⽅插⼊多少像素，使元素向下移动多少像素。

- **bottom** ：表示向元素的下⽅插⼊多少像素，使元素向上移动多少像
  素。

  >  上⾯属性的值可以为负，单位：**px** 。



### 绝对定位(absolute)

> 脱离⽂档流的布局，遗留下来的空间由后⾯的元素填充。
>
> 定位的起始位置为**最近的⽗元素**(postion不为static)，否则为Body⽂档
> 本身。

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228211747.png)







### 相对定位(relative)

> 不脱离⽂档流的布局，只改变⾃身的位置，在⽂档流原先的位置遗留空⽩区域。
>
> 定位的起始位置为**此元素原先在⽂档流的位置**。



![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228212023.png)



### 固定定位(fix)

>  类似于absolute，但不随着滚动条的移动⽽改变位置。

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190228212145.png)



### 默认定位(static)

>  表示此元素为默认定位⽅式。



