---
title:  JavaScript 冒泡事件
date: 2018-12-19 16:21:11
updated: 2018-12-19 16:21:11 
mathjax: false
categories: 
tags:
typora-root-url: JavaScript_冒泡事件
typora-copy-images-to: JavaScript_冒泡事件
top: 1
---


# 三、冒泡事件（了解）

## 3.1、什么是冒泡事件

02冒泡事件.html 代码：

两个重叠的div，分别绑定单击事件：

```javascript
<body>
<style>
    #d1{
        width:200px;
        height:200px;
        border:solid 1px #ccc;
        background-color: #ccc;
    }
    #d2{
        width:100px;
        height:100px;
        border:solid 1px #ccffcc;
        background-color: #ccffcc;
    }
</style>

<div id="d1">
    <div id="d2"></div>
</div>

<script>
    //给 d1 绑定单击事件
    document.getElementById('d1').onclick = function () {
        alert('d1');
    };
    //给 d2 绑定单击事件
    document.getElementById('d2').onclick = function () {
        alert('d2');
    };
</script>

</body>
```

展示效果：

![1532745074426](1532745074426.png)

当点击内层（绿色）div的时候，不但会触发绿色div的单击事件，也会触发底层灰色div的单击事件。

这种透过元素触发另一个元素的事件的情况，就叫做**冒泡事件**。



## 3.2、阻止冒泡事件的发生

标准浏览器使用  `evt.stopPropagation();  `    evt指的是事件对象

IE内核浏览器使用  ``window.event.cancelBubble = true;  ``



02冒泡事件.html  代码：

```html
<body>
<style>
    #d1{
        width:200px;
        height:200px;
        border:solid 1px #ccc;
        background-color: #ccc;
    }
    #d2{
        width:100px;
        height:100px;
        border:solid 1px #ccffcc;
        background-color: #ccffcc;
    }
</style>

<div id="d1">
    <div id="d2"></div>
</div>

<script>
    //给 d1 绑定单击事件
    document.getElementById('d1').onclick = function () {
        alert('d1');
    };
    //给 d2 绑定单击事件
    document.getElementById('d2').onclick = function (e) {
        alert('d2');
        /*************** 阻止冒泡事件发生 **********/
        if(window.event){
            window.event.cancelBubble = true;
        }else{
            e.stopPropagation();
        }
    };
</script>

</body>
```



