我们先生成单选框

```javascript
		<label class="radio-item">
            <input type="radio" name="a">
            <span>男</span>
        </label>
        <label class="radio-item">
            <input type="radio" name="a">
            <span>女</span>
        </label>
```
生成的单选框是这样的![在这里插入图片描述](https://img-blog.csdnimg.cn/20200420212603571.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
看起来并不美观，但是表单元素又是H5默认样式，没办法更改单选框的属性，那么如何更改单选框样式呢
其实有很多种方法，现在我们来利用CSS更改表单单选框的样式

 - 首先在input后面添加空的span样式，然后将空的span样式生成新的单选框，再把input单选框隐藏就行了。
 

```javascript
		 <label class="radio-item">
            <input type="radio" name="a">
            <span class="radio"></span>
            <span>男</span>
        </label>
        <label class="radio-item">
            <input type="radio" name="a">
            <span class="radio"></span>
            <span>女</span>
        </label>
```
添加css样式

```javascript
	.radio-item .radio{
	//定义单选框边框
        display: inline-block;
        width: 12px;
        height: 12px;
        border:1px solid #999;
        border-radius: 50%;
    }
    .radio-item input:checked+.radio{
    //更改单选框选中颜色
        border-color:#008c8c ;
    }
    .radio-item input:checked+.radio::after{
    //在选中单选框里面添加一个小圆心
        content: "";
        display: block;
        width: 6px;
        height: 6px;
        border-radius: 50%;
        background: #008c8c;
        margin-top:3px ;
        margin-left: 3px;
    }
    .radio-item input:checked~span{
    //将文字颜色变成定义颜色
        color: skyblue;
    }
    .radio-item input[type="radio"]{
    //隐藏单选框
        display: none;
    }
```

效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200420213444782.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)