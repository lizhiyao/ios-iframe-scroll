最近在做丁香园调查派抽奖页面时，踩到了一个“IOS上iframe的滚动条失效”的坑。解决方案记录如下：

# 问题描述

在iphone，ipad等设备上设置了iframe高度，倘若iframe的内容足够长超出了iframe设定的高度时，iframe内部html的滚动条不出现。

# 解决方案

在iframe外加一层div，设置样式-webkit-overflow-scrolling:touch; overflow: scroll; 
让超出div的内容可以通过touch来滚动。

# 示例代码

父页面

    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <title>ios iframe srcoll</title>

        <style>
            .warpper {
                overflow: auto;
                -webkit-overflow-scrolling: touch;
                width: 500px;
                height: 500px;
                margin: 100px auto;
                border: 1px solid red;
            }
            
            iframe {
                width: 100%;
                height: 100%;
            }
        </style>
    </head>

    <body>

        <div class="warpper">
            <iframe src="./iframe.html" frameborder="0" scrolling="yes">

            </iframe>
        </div>

    </body>

    </html>
    
被嵌入iframe的页面

    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <title>Document</title>

        <style>
            .content {
                width: 400px;
                height: 1600px;
                border: 1px solid green;
            }
            
            /*重置了滚动条样式，如果项目不需要，可删掉以下三条css规则*/
            body::-webkit-scrollbar {
                width: 6px;
            }
            
            body::-webkit-scrollbar-track {
                border-radius: 200px;
                background-color: #dde4e6;
            }
            
            body::-webkit-scrollbar-thumb {
                background-color: #9fa9ac;
                border-radius: 200px;
            }
        </style>
    </head>

    <body>
        <div class="content">

        </div>
    </body>

    </html>
    
# -webkit-overflow-scrolling

## 摘要

-webkit-overflow-scrolling 属性控制元素在移动设备上是否使用滚动回弹效果.

## 取值

auto

使用普通滚动, 当手指从触摸屏上移开，滚动会立即停止。

touch

使用具有回弹效果的滚动, 当手指从触摸屏上移开，内容会继续保持一段时间的滚动效果。
继续滚动的速度和持续的时间和滚动手势的强烈程度成正比。同时也会创建一个新的堆栈上下文。

## 浏览器兼容性

移动版 Safari  iOS 5.0+


# 参考

[CSS overflow 属性](http://www.w3school.com.cn/cssref/pr_pos_overflow.asp)

[Iframe scrolling iOS 8](http://stackoverflow.com/questions/26046373/iframe-scrolling-ios-8)

[Scroll IFRAMEs on iOS](https://davidwalsh.name/scroll-iframes-ios)

[Testing iOS IFrame and Div Overflow behaviour](http://dev.magnolia-cms.com/~czimmermann/blog/ipad-iframe/iframe1-tall.html)