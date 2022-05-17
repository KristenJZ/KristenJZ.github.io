---
title: "技术：修改HTML网页背景的方法整理"
date: 2022-05-18T06:35:14+08:00
author: "KristenJZ"
slug: Change-html-background-color
draft: false
toc: true
---

## 设置单色背景

文件中添加<style></style>标签，并在其中修改背景

```html
<!DOCTYPE html>
<html>
<head>
  
<style>
  body {   #说明这部分的背景色是什么颜色
    background-color:#93B874; #或是red/green等名称
    }
  h1{     #说明网页标题区的背景是橙色
    background-color:orange;
  }
  p{			#说明这个段落背景颜色是红色
    background-color:red;
  }
 </style>
  </head>
  <body>
  </body>
</html>
```

## 设置图片背景

仍然在<style></style>中作文章，用background-image:

```html
<!DOCTYPE html>
<html>
  <head>
    
    <style>
      body{background-image:url("xxx.png");
      }
    </style>
  </head>
</html>
```

如果想实现图片叠加效果：

```html
<!DOCTYPE html>
<html>
  <head>
    
    <style>
      body{background-image:url("xxx.png"),url2("xxx.gif");
      }
    </style>
  </head>
</html>
```

## 设置渐变背景

background:linear-gradient(方向或角度#direction/angle，颜色1，颜色2，颜色3)

1. 垂直渐变：

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      html{
        min-height:100%
      } #设置这个参数的意义在于，确保渐变效果填充整个页面
      body{
          /* Chrome 10+, Safari 5.1+ */
    background: -webkit-linear-gradient(left,#93B874, #C9DCB9); 
    /* Opera 11.1+ */
    background: -o-linear-gradient(right,#93B874, #C9DCB9); 
    /* Firefox 3.6+ */
    background: -moz-linear-gradient(to right,#93B874, #C9DCB9); 
    /* 标准语法（一定要放在最后）*/
    background: linear-gradient(#93B874, #C9DCB9); 
    /*最好设置一个背景颜色，万一渐变效果加载失败，背景也不会是空白的*/
    background-color: #93B874; 
      }
    </style>
  </head>
  <body>
  </body>
</html>
```

2. 其他属性调整渐变效果

   - 举个例子，你不但可以添加2种以上的颜色，还能在每种颜色后面加上百分比，设置每种颜色的间距。

     ```html
     background: linear-gradient(#93B874 10%, #C9DCB9 70%, #000000 90%);
     ```

   - 给颜色添加透明效果。这会让颜色慢慢褪去。让同一种颜色从彩色变成完全透明。你需要用rgba()功能定义颜色。最后一个值表示透明度，0是完全不透明，1是完全透明。

     ```html
     background: 
     linear-gradient(to right, rgba(147,184,116,0), rgba(147,184,116,1));
     ```

