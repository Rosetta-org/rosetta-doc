## 入门使用文档
从这里开始你可以一步步的了解，如何通过Rosetta提供的接口

### 定义element
定义一个element，需要定义三个部分
- HTML
- CSS
- JavaScript

> Step one

这三个部分用标签```<element></element>```包裹
- 此标签必须的属性为name，作为此element的custom element名称
- name 必须符合Web Components的要求包含'-'

定义一个名为'r-slider'的element的示例：

```html
<element name="r-slider">


</element>
```

> Step two

### 增加html、变量、属性
以```<template></template>```包裹html的内容

```html
<element name="r-slider">
    <template>
    </template>
</element>

```
- 为html增加DOM结构

```html
<element name="r-slider">
    <template>
        <div>
            我是DOM结构示例
        </div>
    </template>
</element>

```

- html中使用数据
    - 如果element有初始化属性为text，可通过```{attrs.text}```引用，同时可以通过实例的update()函数实现数据更新和UI渲染。attrs为内置变量，在js部分会详细说明

    - 如果element的register函数中定义了变量title，可以通过```{title}```直接访问。具体变量的定义和register函数在js部分会详细说明


- html中使用属性

```
<element name="r-slider">
    <template>
        <div>
            我是DOM结构示例
        </div>
        <span>{attrs.text}</span>
    </template>
</element>

```

- html中使用变量

```
<element name="r-slider">
    <template>
        <div>
            我是DOM结构示例
        </div>
        <span>{text}</span>
        <span>{title}</span>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            properties: {
                text: 'text'
            },
            title: '我是一个作用域内的变量'
        });

    </script>
</element>

```

> Step three


### 设置样式
- 定义element时，可以为其定义样式，样式通过内联形式定义
- 支持``` :host```选择器，选择对象是element实例的根节点，以实现内部样式隔离于element外部


```html
<element name="r-slider">
    <style>
        :host div {
            color: red;
        }
    </style>
    <template>
        <div>
            我是DOM结构示例
        </div>
    </template>
</element>

```

> Step four

### 注册element定义逻辑
- js部分用```<script></script>```包裹
- 通过Rosetta.register接口注册element
- Rosetta.register第一个参数为注册的element的名字，第二个参数为自定义渲染函数，在created之前执行
- 第一个参数element的名称需要和```<element></element>```上定义的name保持一致
- 第二个参数自定义渲染函数的arguments为element实例用'tag'表示
- 第二个参数自定义渲染函数和html引用的属性、变量共享作用域


```html
<element name="r-slider">
    <style>
        :host div {
            color: red;
        }
    </style>
    <template>
        <div>
            我是DOM结构示例
        </div>
        <span>
            {title}
        </span>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            title: '我是一个测试title'
        });
    </script>
</element>

```



### 绑定事件
Rosetta为element内部DOM提供事件绑定方式，以'on'加首字母大写的事件名为attribute名，以```{xxx}```定义callback，如下示例：
```
<element name="r-slider">
    <style>
        :host div {
            color: red;
        }
    </style>
    <template>
        <div>
            我是DOM结构示例
        </div>
        <span>
            {title}
        </span>
        <div onClick={clicked}>
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            clicked: function () {
                alert('clicked');
            }
        });
    </script>
</element>
```


### 生命周期
Rosetta为custom elements实现了和标准一致的生命周期：
- created：组件创建
- attached：组件渲染到document里
- detached：组件从document移除
- attributechanged：属性更新

element定义的时候可以绑定生命周期的事件
- onCreated
- onAttached
- onDetached
- onAttributeChanged

组件初始化的生命周期顺序
- created
- internal DOM initialized
- domReady
- attached

提供定义生命周期callback的两种形式
- 可以通过设置DOM的attribute的形式声明对于生命周期的绑定，类似于事件绑定，区别在于以attributes声明的时候生命周期只可以声明在```<element></element>```的属性上
- 在register的函数中定义

示例如下，分别用两种方式声明```attached```和```created```：

```
<element name="r-slider" onAttached={attached}>
    <style>
        :host div {
            color: red;
        }
    </style>
    <template>
        <div>
            我是DOM结构示例
        </div>
        <span>
            {title}
        </span>
        <div onClick={clicked}>
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            attached: function () {
                alert('attached');
            },
            created: function() {
                alert('created');
            },
            clicked: function() {
                alert('clicked');
            }
        });
    </script>
</element>
```



### 声明依赖
Rosetta在使用custom element时，使用HTML Import声明依赖，如下示例：

```
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <link rel="import" type="text/html" href="r-slider.html">
</head>
<body>

    <r-slider></r-slider>
</body>
</html>
```


### 更新element的属性
- 在custom element使用的时候用attributes设置属性初始值
- 通过element实例的update函数接口更新属性值，Rosetta自动完成UI更新
- 内部html中通过```{attrs.xxx}```来引用对于```xxx```属性的


定义element，绑定事件、实现属性更新逻辑
```html
<element name="r-slider">
    <style>
        :host div {
            color: red;
        }
    </style>
    <template>
        <div>
            我是DOM结构示例
        </div>
        <span>
            {title}
        </span>
        <div onClick={clicked}>
            {attrs.text}
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            properties: {
                text: 'init'
            },
            clicked: function() {
                this.update({
                    text: 'clicked!'
                })
            }
        });
    </script>
</element>

```

使用element，在使用处用HTML Import声明依赖
```
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <link rel="import" type="text/html" href="r-slider.html">
</head>
<body>

    <r-slider text="我是一个属性测试"></r-slider>
</body>
</html>
```


### refs快速访问内部DOM
通过tag的refs属性快速访问DOM，作为对dom查询接口的补充，返回值为DOM对象

示例如下：

```html
<element name="r-slider">
    <style>
        :host div {
            color: red;
        }
    </style>
    <template>
        <div ref='test'>
            我是ref的DOM选择示例
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            attached: function() {
                var test = this.$['test'];
                test.innerHTML += '更新啦';
            }
        })
    </script>
</element>
```

### 定义容器
- 在custom element内部通过```<content></content>```定义容器
- 为```<content></content>```加上属性select设置对于element实例的子元素的过滤
- 比如一个```select```为'.aaa'的content，表示只有具有类名为'aaa'的子元素可以放入容器中，其他的子元素会被丢弃忽略

示例如下：

定义content
```html
<element name="r-slider">
    <style>
        :host div {
            color: red;
        }
    </style>
    <template>
        <content select='.aaa'>
        </content>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider'
        })
    </script>
</element>

```


使用element，传入子元素
```
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <link rel="import" type="text/html" href="r-slider.html">
</head>
<body>
    <r-slider text="我是一个属性测试">
        <div class="aaa">
            我会被选择加入容器
        </div>
        <div>
            我会被忽略
        </div>
    </r-slider>
</body>
</html>
```

### 嵌套使用element
在定义elementA的时候使用已经定义好的elementB，是这里说的"嵌套使用element"
按照以下步骤嵌套使用element

- 通过HTML Import引入依赖的elementB定义文件
- 使用elementB的标签

示例如下：
```html
<element name="r-a">
    <style>
        :host div {
            color: red;
        }
    </style>
    <link rel="import" type="text/html" href="r-b.html">
    <template>
        <content select='.aaa'>
        </content>
        <r-b></r-b>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-a'
        });
    </script>
</element>

```

### ready接口
- 在当前页面所有的custom element实例化完毕的时候会执行Rosetta ready状态的callback
- Rosetta.ready接口接受function为参数作为callback
- Rosetta.render()会主动触发element渲染，从而触发Rosetta.ready的callback的执行

```
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <link rel="import" type="text/html" href="r-slider.html">
</head>
<body>
    <r-slider text="我是一个属性测试">
        <div class="aaa">
            我会被选择加入容器
        </div>
        <div>
            我会被忽略
        </div>
    </r-slider>

    <script type="text/javascript">
        Rosetta.ready(function() {
            //you can access element instance and do something here
        });
    </script>
</body>
</html>
```



### ref接口快速element实例
- 以声明的方式使用element的时候，可以添加ref这个attribute
- 通过Rosetta.ref('refName')快速获取element实例对象

```
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <link rel="import" type="text/html" href="r-slider.html">
</head>
<body>
    <r-slider text="我是一个属性测试" ref="lalala">
        <div class="aaa">
            我会被选择加入容器
        </div>
        <div>
            我会被忽略
        </div>
    </r-slider>

    <script type="text/javascript">
        Rosetta.ready(function() {
            //you can access element instance and do something here

            var slider = Rosetta.ref('lalala');
        });
    </script>
</body>
</html>
```


### init接口
Rosetta提供init接口，内部调用，进行页面自定义tag的解析


```
    Rosetta.init()
```


### 基于FIS3的预处理
- Rosetta提供基于FIS3的解析插件进行element的定义html文件解析和编译
- Rosetta提供基于FIS3的打包插件，对于项目依赖的element进行按element对页面依赖关系进行插入，或者按页面级的allInOne打包后插入
- 构建配置在fis-conf.js中配置

示例配置如下：

```
fis
    .match('*.{html,tpl}', {
        parser: fis.plugin('rosetta', {
            compileUsage: false
        })
    })

    .match('/elements/r-*.html', {
        rExt: '.js'
    })
    .match('/elements/*.*', {
        release: '/static/$0'
    })
    .match('::packager', {
        postpackager: fis.plugin('rosetta', {
            allInOne: true
        })
    });

```
详细配置参考[脚手架](./beginning/scaffold.md)中的具体项目示例
