---
title: 前端CSS基础——行盒模型与行块盒模型
---
### 行盒模型
行盒模型是display属性为inline的元素，常见的行盒元素有a、span、strong、em、video、audio、img等。
行盒模型与块盒模型的不同特点有：

 1. 行盒模型不独占一行，块盒模型独占一行。
 2. 块盒模型可对上下左右方向进行填充，行盒模型只能对水平方向进行填充。
 3. 行盒模型无法设置宽高，只能通过调整字体大小、行高等进行间接调整。

### 行盒模型的盒子属性

 1. 内边距：只有水平方向设置有效，垂直方向设置无效。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408180649241.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408180707553.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
 2. 内边距：水平方向有效，垂直方向无效。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408180901885.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408180915751.png)
 3. 边框：水平方向有效，垂直方向无效。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020040818120370.png)

### 行块盒
#### 什么是行块盒
行块盒是display属性为inline-block的元素，它既有行盒的特点又有块盒的特点，它不独占一行，但盒子模型的所有尺寸又可用，例如width、height属性都可用。

#### 行块盒的简单应用
行块盒比较常用于页面的分页，例如百度页面的分页
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408182226308.png)
#### 实现网页的分页

```javascript
//css
.test a{
        border: 1px solid #e1e2e3;
        color: #38f;
        text-decoration: none;
        width: 34px;
        height: 34px;
        display: inline-block;
        text-align: center;
        line-height: 34px;
    }
   .test a:hover{
        background: #f2f8ff;
        border: 1px solid #38f; 
    }
    .test .select{
        border:1px none;
        color: black;
    }

//body
<div class="test">
       <a class="select" href="">1</a>
       <a href="">2</a>
       <a href="">3</a>
       <a href="">4</a>
       <a href="">5</a>
       <a href="">6</a>
       <a href="">7</a>
       <a href="">8</a>
       <a href="">9</a>
   </div>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408183939314.png)
