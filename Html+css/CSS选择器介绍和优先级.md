# CSS选择器介绍和优先级

### 选择器权重及优先级 

权重分为四级，权重值越大优先级越高。

1. 内联样式。如：style=“xxx”，权值为1000
2. ID选择器。如：#content，权值为100
3. 类，伪类和属性选择器。如：.content,:hover,[attribute],权值为10
4. 元素选择器，伪元素选择器。如：div,p,权值为1

**注意：通用选择器（\*），子选择器（>）和相邻同胞选择器（+）并不在这四个等级中，所以他们的权值都为0。**

> **【以上摘自网络】**

---------------------------

### 内联样式

```html
<h1 style="color: red;">CSS选择器</h1>
```

### ID选择器

`css`

```css
 #ID_choose{
        color: black;
 }
```

`html`

```html
<h1 id="ID_choose" >CSS选择器</h1>
```

### 类选择器

`css`


```css
 #Cls_choose{
        color: yellow;
 }
```

`html`

```html
<h1 class="Cls_choose" >CSS选择器</h1>
```
### 元素选择器

`css`

```css
 h1{
        color: green;
 }
```

`html`

```html
<h1  >CSS选择器</h1>
```




下面我准备来验证一下

将 **内联样式、ID选择器、class选择器、元素选择器** 四种进行两两比较。emmm，那么就是

