---
title: 前端HTML进阶和CSS基础——表格元素
---
### 表格元素
当今的开发中表格元素应用得并不多，属于比较老的一个元素，但在CSS出现之前，整个网页的布局通常都是用表格元素来实现的。之所以现在应用不多，是因为表格元素的渲染速度过慢，不适合当前的网页布局。但表格元素也不是完全被淘汰，在一些网页的后台页面（管理员页面）还是用表格元素布局得比较多（方便）。下面用实例来快速了解表格元素。

#### 表格元素的语义化书写
表格元素（table）的主体如图所示，标题在顶部位置，默认居中；tr表示行，有几个tr就有几行；th和td一样，只是书写规范不一样，td表示有几列，tr里面有几个td就表示这一行有几列。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200420130152591.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
表格元素语义化的书写，也可不用语义化书写，显示效果一样，但是开发者应该养成良好的语义化书写习惯，这样也更有利于代码的可维护性。

```javascript
    <table>
    	<caption></caption>
        <thead>
            <tr>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td></td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td></td>
            </tr>
        </tfoot>
    </table>
```

#### 定义一个表格元素
定义一个表格标题为**数据表**，表头为1行5列，表格主体为10行5列，表尾为一行一列的表格，按顺序执行

 1. 先定义表格标题（option）
 2. 定义表头（1个tr，里面5个th）
 3. 定义表格主体（10个tr，每个tr里面有5个td）
 4. 定义表尾（1个tr，1个td，td添加属性colspan合并多余的列）

看看代码

```javascript
<table>
        <caption>数据表</caption>
        <thead>
            <tr>
                <tr>
                    <th>表头1</th>
                    <th>表头2</th>
                    <th>表头3</th>
                    <th>表头4</th>
                    <th>表头5</th>
                </tr>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>数据1</td>
                <td>数据2</td>
                <td>数据3</td>
                <td>数据4</td>
                <td>数据5</td>
            </tr>
           ......
           	省略8个tr
           ......
            <tr>
                <td>数据1</td>
                <td>数据2</td>
                <td>数据3</td>
                <td>数据4</td>
                <td>数据5</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="5">合计</td>
            </tr>
        </tfoot>
    </table>
```
图片效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200420184155308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
这就是一个完整的表格了，但是看起来并不美观，所以我们可以简单美化一下

#### 表格元素的美化

 1. 定宽，附加边框效果

```javascript
//添加css样式
table{
        width: 100%;
    }
    th,td{
        border: 1px solid #ccc;
    }
```
效果（为了显示全部表格，网页缩小50%）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200420184454931.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

 2. 合并边框间距，并给标题设置加粗，调整td行高并居中
 

```javascript
	table{
        width: 100%;
        border-collapse: collapse;//合并边框间隙
    }
    table caption{
        font-size: 2em;
        font-weight: bold;
        padding: 20px 0;
    }
    th,td{
        border: 1px solid #ccc;
        text-align: center;
        padding: 20px 0;
    }
```
效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200420184545341.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

 3. 添加表头背景颜色，优化表体背景颜色

```javascript
	table thead{
        background-color:#008c8c;
        color: #fff;
    }
    table tbody tr:nth-child(odd){//添加表体偶数的tr背景颜色
        background-color: #eee;
    }
```
效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200420181049289.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

 4. 添加鼠标移动到对应行变色效果

```javascript
	table tbody tr:hover{
        background-color: #ccc;
    }
```

效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200420181621591.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

 5. 表尾单元格设置水平向右

```javascript
	tfoot td{
        padding-right: 250px;
        text-align: right;
    } 
```
完成后整体效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200420184842507.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)