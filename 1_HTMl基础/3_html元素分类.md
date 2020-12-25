# HTML 元素分类

## 默认样式分类

- 块级元素(block) 独占一行

  div ｜ P

- 行内元素(inline) 允许共存

  span | strong | i

- inline-block(对外是行内元素，允许共存。但是自身拥有高度等属性)

  input

## 按内容分

[官网说明](https://www.w3.org/)

## HTMl 元素嵌套关系

- 块级元素可以包含行内元素
- 块级元素不一定能包含块级元素
- 行内元素 一般 不能包含块级元素

  但是 a>div 是合法的

## HTML 元素默认样式

### CSS reset

- 重写方法

  [解决方案](https://meyerweb.com/eric/tools/css/reset/)

- 粗暴重置

  ```labguage=html
  <style>
    *{
      margin:0;
      padding:0
    }
  </style>
  ```
