# sass

标签（空格分隔）： 新技术

---

> 预处理，使用非css语法的变量，嵌套，继承等；

1. 变量

   以`$`开头的变量，来表示属性值；在样式表中的css正常语法引用；


        $font-stack:Helvetica, sans-serif;
        
        $primary-color: #333;
        
        body {
             font: 100% $font-stack;
     color: $primary-color;
     
        }
        

编译后：

    body {
      font: 100% Helvetica, sans-serif;
      color: #333;
    }
2. 嵌套

可以使你像html文档中层级分明的写样式。

        nav {
           ul {
                margin: 0;
                padding: 0;
                list-style: none;
             }

            li { display: inline-block; }

            a {
                display: block;
                padding: 6px 12px;
                text-decoration: none;
            }
        }
        
    
编译后：

    nav ul {
        margin: 0;
        padding: 0;
        list-style: none;
    }

    nav li {
            display: inline-block;
        }

    nav a {
            display: block;
            padding: 6px 12px;
            text-decoration: none;
    }
    
    
    
3. @import的方式引用碎片



        // _reset.scss

        html,
        body,
        ul,
        ol {
             margin: 0;
            padding: 0;
        }


     
         //  base.scss
        @import 'reset';

         body {
                font: 100% Helvetica, sans-serif;
                background-color: #efefef;
            }
            
            
编译后：

    html, body, ul, ol {
                    margin: 0;
                    padding: 0;
    }

    body {
        font: 100% Helvetica, sans-serif;
        background-color: #efefef;
    }
4. 自动复用前缀

使用@mixin+name,用@include引入此变量。

        @mixin border-radius($radius) {
    -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
            }

    .box { @include border-radius(10px);}
    
编译后：
    
    .box {
      -webkit-border-radius: 10px;
      -moz-border-radius: 10px;
      -ms-border-radius: 10px;
      border-radius: 10px;
    }
5. 继承

可以共用一些css属性。直接在样式中使用：@extend+样式名。

    .message {
      border: 1px solid #ccc;
      padding: 10px;
      color: #333;
    }
    
    .success {
      @extend .message;
      border-color: green;
    }
    
    .error {
      @extend .message;
      border-color: red;
    }
    
编译后：
 
     .message, .success, .error{
      border: 1px solid #cccccc;
      padding: 10px;
      color: #333;
    }
    
    .success {
      border-color: green;
    }
    
    .error {
      border-color: red;
    }   
6. 使用运算
`+, -, *, /, and %`

.container{ width: 100%;}    
    
    article[role="main"] {
      float: left;
      width: 600px / 960px * 100%;
    }
    
    aside[role="complimentary"] {
      float: right;
      width: 300px / 960px * 100%;
    }


编译后：

    .container {
      width: 100%;
    }
    
    article[role="main"] {
      float: left;
      width: 62.5%;
    }
    
    aside[role="complimentary"] {
      float: right;
      width: 31.25%;
    }
    
    
    


  
  配合[koala](http://www.w3cplus.com/preprocessor/sass-gui-tool-koala.html) 使用，简直了~