---
title: 前端CSS基础——浮动布局与高度坍塌
---
### 浮动布局
浮动布局是CSS布局中的三大布局方式之一，也是页面开发中常用的布局，经常应用于文字环绕与横向排列中，在大部分网页中的横向排列都是用浮动实现的,例如

> **横向排列**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200411223954642.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
> **文字环绕**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200411224156405.png)

#### 浮动的特点

 - 要将元素变成浮动盒子，只需要修改**float**属性即可
	 - **left**：左浮动，元素靠上靠左排列
	 - **right**：右浮动，元素靠上靠右排列
 - 当一个元素浮动后，元素必定为块盒
 - 浮动盒子的包含块在绝大部分情况下是父类元素的内容盒
 - 浮动盒子在排列时会避开常规流块盒
 - 常规流块盒在排列时会无视浮动元素块盒

举例说明：

> 左浮动排列
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200411230307447.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
右浮动排列
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200411230336212.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
浮动盒子遇到常规流块盒（在1号浮动盒子前加入常规流块盒，浮动盒子避开常规流块盒进行排列）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200411230642788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
常规流块盒遇到浮动盒子（在10号浮动盒子后加入常规流，常规流无视浮动盒子进行排列）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200411230754930.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
在1~10号浮动盒子之间加入常规流（例如在4号盒子后面加入常规流块盒）
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020041123091892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)



#### 盒子的尺寸

 - 宽度：**auto**表示适应内容宽度
 - 高度：**auto**表示适应内高度
 - margin：**auto**值为0
 - 百分比值：相对包含块宽度的百分比

### 高度坍塌
#### 高度坍塌的问题
**高度坍塌是多数情况的网页布局样式混乱的根源**
 -  为什么会高度坍塌
 常规流块盒未设置固定高度，在排列时常规流块盒不会考虑浮动盒子的高度，从而导致常规流块盒高度不填充。
 例如：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200411231830893.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
 
#### 高度坍塌的解决方法
要解决高度坍塌的方法，需要用**clear**属性来**清除浮动**，清除浮动是指**应用该属性的元素，必须出现在前面所有浮动盒子的下方。**
 - **clear：none**:默认值，不清除浮动
 - **clear：left**：清除左浮动
 - **clear：right**：清除右浮动
 - **clear：both**：清除浮动

那么该如何解决高度坍塌问题呢，有2种方法

 1. 在所有浮动盒子后面加入一个空的块盒，引入样式

```
.自定义{
	clear:both;
}
```

2. 利用伪元素选择器**after**来对包含块添加样式

```
.自定义：：after{
	content:"";
	display:block;
	clear:both;
}
```
举例说明

```
	.float{
        background: skyblue;
        width: 500px;
        /* height:300px; */
        padding: 30px 0;
    }
    .float .item{
        background: #008c8c;
        width:50px;
        height:50px;
        float: left;
        margin: 0px 10px 10px 10px;
        text-align: center;
        line-height: 50px;
        border: 1px solid;
    }
    
	<div class="float">
        
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
        <div class="item">6</div>
        <div class="item">7</div>
        <div class="item">8</div>
        <div class="item">9</div>
        <div class="item">10</div>
        
    </div>
```
方法一：

```
.clearfix{
	clear:both;
}
在10号浮动盒子下面加入空块盒，并引入样式clear
<div class="clearfix"></div>
```

方法二：

```
定义清除浮动样式
.clearfix::after{
	content:"";
	display:block;
	clera:both;
}
再在父类div中添加清除浮动样式
<div class="float clearfix">
...
</div>
```
得到结果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200411234521691.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)