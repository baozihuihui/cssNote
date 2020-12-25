# Scss

## 嵌套

- 允许将子类直接写到父类的样式中，形成强约束
- & 表示当前所在样式的元素，可以用于元素选择器

```language=scss
.warpper{
    background:white;

    .nav{
        font-size:12px;
    }
    .content{
        font-size:14px;
        &:hover{
            background:red;
        }
    }
}

```

## 变量

- 变量使用 $ 作为开始
- 数字必须要带参数
- 允许在样式中进行二次运算，注意乘法不需要数字

```language=scss
@fontsize:14px;
@bgcolor:red;
.warpper{
    background:lighten(@bgcolor,40%);

    .nav{
        font-size:@fontsize;
    }
    .content{
        font-size:@fontsize + 2px;
        &:hover{
            background:@bgcolor;
        }
    }
}

```

## mixin

- 类似于 JS 函数调用
- 显示声明 @mixin
- 调用 需要 @include 进行调用

```language=scss

$fontsize:14px;
$bgcolor:red;

@mixin block($fontsize){
    background:lighten($bgcolor,40%);
    font-size:$fontsize;
}
.warpper{
    background:lighten($bgcolor,40%);

    .nav{
        @include block($fontsize);
    }
    .content{
        @include block($fontsize + 2px);
        &:hover{
            background:$bgcolor;
        }
    }
}

```

## extend

- 继承选择器,不可变，可以在 CSS 提起公共样式，减少重复代码
- 显示声明 @extend 类型选择器

```language=scss

$fontsize:14px;
$bgcolor:red;

.block{
    background:lighten($bgcolor,40%);
    font-size:$fontsize;
}
.warpper{
    background:lighten($bgcolor,40%);

    .nav{
        @extend .block;
        color:#333
    }
    .content{
        @extend .block;
        &:hover{
            background:$bgcolor;
        }
    }
}

```

### loop

- 通过循环生成一系列样式
- 使用 @for $i from 1 through n 执行循环
- mixin 递归中 通过 @if $n > 0 也就是 当 n 大于 0 就结束 设定执行条件
- 变量名称可以作为选择器名称的一部分。 .col-#{$n}

```language=scss
@for $i form 1 through 12{
    .col-#{$i}{
        width:1000px / 12 * $n
    }
}

// 使用 mixin 递归
@mixin gen-col($n){
    @if $n > 0{
         @include($n-1);
         .col-#{$n}:{
             width:1000px / 12 * $n
         }
    }
}

@include gen-col(12)

```

### import

- 将引入编译到同一个文件中，减少 css 请求文件数
- 只要正常引入模块文件后，变量可以直接跨文件使用

**_a.scss_**

```language=scss
$fontsize:12px
```

**_b.scss_**

```language=scss
$import 'a'

.content{
    font-size:$fontsize
}

```
