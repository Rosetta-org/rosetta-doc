## DOM结构
模板语法以```{}```包裹jsx形式作为模板语法，以下是关于模板的几个方面

### 数据和DOM结构
- 简单的'title'变量
```
    <template>
        {title}
    </template>
```
- 复杂的模板拼接，用闭包包裹内部结构

```
    <template>
        {
            (function() {
                return (
                    <div>
                        <span>{title}</span>
                    </div>
                )
            })
        }
    </template>
```

```
    <template>
        {
            [1,2,3].map(function(item, index) {
                return (<div>{item}</div>)
            })
        }
    </template>
```

### 查找DOM
```
<template>
    <div ref="aaa">
        ref的测试
    </div>
</template>
<script type="text/javascript">
    Rosetta({
        is: 'r-test',
        attached: function() {
            this.$.aaa // 访问属性为ref="aaa"的dom元素，或者 this.$['aaa']
        }
    })
</script>
```
在定义组件的模板内，设置DOM的attribute的ref值，通过$可以访问


### 容器DOM的使用
使用<content></content>挖一个容器的坑，使用attribute为select设置能通过此容器过滤的选择器

```
<element name="r-test">
    <style>
        :host {

        }
    </style>
    <template>
        <div ref="aaa">
            ref的测试
        </div>
        <content select=".test">
        </content>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-test',
            attached: function() {
                this.$.aaa // 访问属性为ref="aaa"的dom元素
            }
        })
    </script>
</element>

<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
    <link rel="import" type="text/html" href="r-test.html">
    <r-test>
        <div class="test">
        </div>
    </r-test>
</body>
</html>
```


