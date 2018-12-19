---
title: [JavaScript]阻止默认行为
date: 2018-12-19 16:21:11
updated: 2018-12-19 16:21:11 
mathjax: false
categories: 
tags:
typora-root-url: .
typora-copy-images-to: .
top: 
---


# 四、阻止默认行为（了解）

**默认行为**就是html标签的一些默认行为，比如点击a标签会跳转，比如点击了submit按钮表单会提交。这些都属于标签的默认行为。

有些时候，点击了a标签或者submit按钮后不希望执行标签的默认行为，这时候就需要阻止默认行为。



**阻止默认行为：**

标准浏览器：`evt.preventDefault();`

IE内核浏览器：`window.event.returnValue = false;`



03阻止默认行为.html

```html
<body>

<a href="02冒泡事件.html">冒泡事件</a>

<script>
    //获取a 标签
    document.getElementsByTagName('a')[0].onclick = function (evt) {
        //标准浏览器：evt.preventDefault();
        //IE内核浏览器：window.event.returnValue = false;
        /*if(window.event){
            window.event.returnValue = false;
        }else{
            evt.preventDefault();
        }*/
        //最简单的返回是直接 return false;
        return false;
    };
</script>

</body>
```

**延伸：**

1. 在实际开发中，敏感操作一定要给提示。

```html
<a href="02冒泡事件.html" onclick="return confirm('你确定要删除吗');">删除</a>
```

2. 检测表单提交的两种方式

```html
<body>

<form name="myform" action="02冒泡事件.html" method="post">
    用户名：<input type="text" name="username" />
    <input type="submit" name="sub" value="提交" />
</form>

<script>
    //方式一：给submit按钮绑定onclick事件
    /*document.myform.sub.onclick = function () {
        alert('请填写用户名');
        return false; //阻止表单提交
    };*/

    //方式二：给表单form绑定onsubmit事件
    document.myform.onsubmit = function(){
        alert('请再次填写用户名');
        return false; //阻止表单提交
    };
</script>

</body>
```



