##一分钟功能概览
Rosetta让开发者能够更便捷的以声明式来写组件
核心功能custom elements使得开发者编写交互组件和复杂应用的时候更加容易

总体说来Rosetta的custom elements包含一下核心功能
- [引用组件](./core.md#引用组件)
- [注册组件](./core.md#注册组件)
- [内部DOM结构](./core.md#内部DOM结构)
- [组件容器](./core.md#组件容器)
- [生命周期](./core.md#生命周期)
- [事件绑定](./core.md#事件绑定)
- [属性声明](./core.md#属性声明)
- [数据更新](./core.md#数据更新)
- [组件嵌套](./core.md#组件嵌套)


这里你可以看到每个核心功能的例子

### 引用组件
- 使用HTML Import来引入组件、声明组件依赖
- 通过编译环节处理兼容性问题
- 在使用custom element的位置添加如下link标签

引用方式如下：
```
<link rel="import" type="text/html" href="r-slider.html">
```


### 注册组件
- 开发者可以通过Rosetta.register函数注册组件，这些组件可以直接在浏览器中通过标签来使用
- 开发者为注册的组件定义标签名和属性和方法
- 遵循Web Components标准，注册的组件名必须包含'-'

定义：
```html
<element name="r-slider">
    <style>
    </style>
    <template>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            properties: {
                list: {
                    type: Array,
                    value:[
                        {
                            title: '111'
                            src: 'xxx'
                        },
                        {
                            title: '222'
                            src: 'zzz'
                        }
                    ]
                },
                text: {
                    type: String,
                    value: '测试'
                }
            }
        })
    </script>
</element>
```
使用：
```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
    <r-slider text="啦啦啦" list="[]">
    </r-slider>
</body>
</html>
```


### 内部DOM结构
组件可以定义其内部的DOM结构，通过```<template></template>```标签包裹

```html
<element name="r-slider">
    <style>
    </style>
    <template>
        <div>
            {attrs.text}
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            properties: {
                list: {
                    type: Array,
                    value:[
                        {
                            title: '111'
                            src: 'xxx'
                        },
                        {
                            title: '222'
                            src: 'zzz'
                        }
                    ]
                },
                text: {
                    type: String,
                    value: '测试'
                }
            }
        })
    </script>
</element>
```

### 组件容器
组件通过```<content></content>```声明自身的容器，并通过```select```字段作为选择器过滤，比如select='.aaa'的表示只会将当前组件使用时定义的子元素中选择器符合'.aaa'的元素作为实际子元素，其他的会自动忽略，比如

定义
```html
<element name="r-slider">
    <style>
    </style>
    <template>
        <div>
            {attrs.text}
        </div>
        <content select='.aaa'>
        </content>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            properties: {
                list: {
                    type: Array,
                    value:[
                        {
                            title: '111'
                            src: 'xxx'
                        },
                        {
                            title: '222'
                            src: 'zzz'
                        }
                    ]
                },
                text: {
                    type: String,
                    value: '测试'
                }
            }
        });
    </script>
</element>
```
使用：
假如目录结构如下
```
-
- index.html
- elements
    - r-slider.html
```

```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
    <link rel="import" type="text/html" href="elements/r-slider.html">
    <r-slider text="啦啦啦" list="[]">
        <div class="aaa">
            我会被选中
        </div>
        <div>
            我会被忽略
        </div>
    </r-slider>
</body>
</html>
```

### 生命周期
Rosetta为custom elements实现了和标准一致的生命周期：
- created：组件创建
- attached：组件渲染到document里
- detached：组件从document移除
- attributechanged：属性更新


### 属性声明
在组件定义的时候，register函数的第二个参数renderFunction里，可以进行属性默认值的声明
```
<element name="r-slider">
    <style>
    </style>
    <template>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
            properties: {
                list: {
                    type: Array,
                    value:[
                        {
                            title: '111'
                            src: 'xxx'
                        },
                        {
                            title: '222'
                            src: 'zzz'
                        }
                    ]
                },
                text: {
                    type: String,
                    value: '测试'
                }
            }
        });
    </script>
</element>
```

使用组件的时候以attributes的方式进行属性初始化：
```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
    <r-slider text="初始化属性" list="[]">
    </r-slider>
</body>
</html>
```

### 事件绑定
- 组件内DOM支持声明式的原生事件绑定，以'on'加首字母大写的事件名形式绑定事件:

```
<element name="r-button">
    <style>
    </style>
    <template>
        <div onClick={clicktest}>
            测试点击
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-button',
            clicktest: function() {
                alert('clicked');
            }
        })
    </script>
</element>
```

- 组件支持声明式的事件绑定

```
<element name="r-button" onAttached={attachcb}>
    <style>
    </style>
    <template>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-button',
            attachcb: function() {
                alert('clicked');
            }
        })
    </script>
</element>
```


### 数据更新
通过element实例的attachcb接口，进行数据更新，比如在组件渲染完毕的时候进行数据更新

```
<element name="r-button" onAttached={attachcb}>
    <style>
    </style>
    <template>
        <div>
            {text}
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-button',
            properties: {
                text: '测试'
            }
            attachcb: function() {
                this.text = 'after render';
            }
        });
    </script>
</element>
```

### 组件嵌套
Rosetta支持自定义组件的嵌套，使用方式和普通标签一样，组件嵌套有两种情况，一类是定义嵌套，第二类是使用时嵌套
- 组件r-a定义时在r-a.html中使用了组件r-b，注意需要先声明依赖关系```<link rel="import" type="text/html" href="r-b.html">```再使用，否则r-b没加载加载，无法使用

```
    <element name="r-a" onAttached={attachcb}>
        <style>
        </style>
        <template>
            <link rel="import" type="text/html" href="r-b.html">
            <r-b>
                我是被嵌套的组件
            </r-b>
            <div>
                {text}
            </div>
        </template>
        <script type="text/javascript">
            Rosetta({
                is: 'r-a',
                properties: {
                    text: '测试'
                }
                attachcb: function() {
                    this.text = 'after render';
                }
            });
        </script>
    </element>
```

- 写页面结构的时候r-b是r-a的子节点

```
    <!DOCTYPE html>
    <html>
    <head>
        <title></title>
    </head>
    <body>
        <div>测试嵌套</div>
        <r-b>
            <r-a>
                我是被嵌套的组件
            </r-a>
        </r-b>
    </body>
    </html>
```

