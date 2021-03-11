# CSS

# 1 CSS 介绍

层叠样式表(英文全称：Cascading Style Sheets)是一种用来表现[HTML](https://baike.baidu.com/item/HTML)（[标准通用标记语言](https://baike.baidu.com/item/标准通用标记语言/6805073)的一个应用）或[XML](https://baike.baidu.com/item/XML)（标准通用标记语言的一个子集）等文件样式的计算机语言。CSS不仅可以静态地修饰网页，还可以配合各种脚本语言动态地对网页各元素进行格式化。 

CSS 能够对网页中元素位置的排版进行像素级精确控制，支持几乎所有的字体字号样式，拥有对网页对象和模型样式编辑的能力。

现在是CSS 3.0

---

# 2 快速入门

## 2.1 语法

```css
selector{
   statement1;
   statement2;
  /* comments */
}
```



## 2.2 3种导入方式

```html
<!-- 内联CSS -->
   <head>
     <style>
        h1{
            color: blueviolet;
        }
    </style>
</head> 
   
<!-- 外引css（Recommended） -->
<head>
  <link rel="stylesheet" href="css/demo01.css">
</head>    
<!-- 外引css 写法二 导入式，先出骨架再渲染，不好用 -->
<head>
  <style>
    @import url("css/demo01.css");
  </style>
</head>    

<!-- 行内样式 -->
    <h3 style="color: red">标题</h3>
```

## 2.3 优先级

**就近原则**：谁离定义的元素近就听谁的。

## 2.4 三种基本选择器

```css
/* 标签选择器 只能指定一标签 */
h1{
  color: red;
  background: #3cbda6;
  border-radius: 24px;
}

p{
  font-size: 80px;
}

/* 类选择器 */
.className{
  color: red;
  background: #3cbda6;
  border-radius: 24px;
}

.className.className2{
  color: red;
  background: #3cbda6;
  border-radius: 24px;
}

h1.className.className2{
  color: red;
  background: #3cbda6;
  border-radius: 24px;
}

/* ID选择器 全局唯一 */
#Id1{
  color: #ff008a;
}
```

## 2.5 属性选择器

```css
/*属性选择器: 存在id属性的a元素*/
        a[id]{
            background: yellow;
        }

        a[id="first"]{
            background: green;
        }

        /*  *= 包含等于 */
        a[class*="links"]{
            background: green;
        }

        /*  ^= 以什么开头 */
        a[class^="http"]{
            background: gray;
        }

        /*  $= 以什么结尾 */
        a[class$="http"]{
            background: gray;
        }
```



## 2.6 层次选择器

1. 后代选择器: 

   ```css
   body p{
               background: gray;
           }
   /* body 所有后代的p */
   ```

   

2. 子选择器

   ```css
    body>p{
               background: gray;
           }
   /* 儿子p*/
   ```

   

3. 相邻兄弟选择器

   ```css
   /*紧贴这个p下面那个同辈，只有一个，注意相邻*/
   .active + p {
     background: gray;
   }
   ```

   

4. 通用选择器

```css
/*这个p下面所有兄弟元素*/
.active~p{
  background: gray;
}
```

## 2.7 结构伪类选择器

```css
/* ul 的第一个子元素 */
ul li:first-child{
  background: gray;
}

/* ul 的最后一个子元素 */
ul li:last-child{
  background: gray;
}

。。。
```

