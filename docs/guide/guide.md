## 特征和开发指南

Rosetta提供一系列的核心功能和特征，为开发者建立自定义element提供便利，并且让custom element具备标准DOM element所具有的功能。

> 我们首先看一下使用Rosetta定义element的方式

```html
<element name="r-helloworld">
    <style>

    </style>
    <template>
        {hellotext}
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-helloworld',
            properties: {
                hellotext: {
                    type: String,
                    value: 'ssds'
                }
            }
        });
    </script>
</element>
```


> 再回顾一下标准的DOM element具备的特征

- 使用document.createElement创造DOM实例
- DOM element实例可以包含子DOM element
- 可以通过特性和属性进行配置
- 有默认样式、可以自定义样式覆盖默认样式
- 有接口让开发者可以操作内部状态，比如事件等

> 为实现上述功能，Rosetta实现如下几类核心功能

- 类注册和生命周期：提供接口为给定的名称生成对应名称的element类，提供生命周期四阶段接口，为自定义逻辑提供回调点
- element的属性：实现attribute、UI data、property的映射
- 模版：定义element内部DOM结构
- 默认样式和覆盖：设置element默认样式，部分实现样式隔离
- 事件：事件绑定接口机制
- 数据更新：提供数据更新机制，实现attribute、UI data、property之间的数据流动
- 功能函数接口：提供常用的函数，便于实现逻辑



