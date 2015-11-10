## 自定义组件的注册和生命周期定义
这一节介绍了如何注册一个自定义组件，每个组件生命周期是怎么样的

### 注册element
创建一个element前，确保已经为Rosetta注册了这个类型的element。
可以为element类设置以下内容：
- element类型名
- properties，对应于初始化数据传入方式的attributes
- 生命周期相关的接口：created、ready、attached、attributechanged、destroyed
- 其他属性、接口等

注册接口如下：

```js
Rosetta({
    is: 'r-newelement', // 注册接口唯一必填项
    properties: {
        aaa: { // 设置默认值
            type: Array,
            value: [1,2,3,5]
        },
        bbb: Number //不设置默认值的简约写法
    },
    foo: 'dsd',
    po: function() {
        // xxx
    }
});

```

### 生命周期
组件化和模块化是常常提到的用于优化代码组织形式的方式，但是有时候大家会模糊这两者的差别。模块化更偏向一种物理的组织；而组件化则需要能满足功能明确、接口清晰、从创建到销毁完整进化能力。
因此生命周期是组件化的一大特征，webcomponents标准定义了四个阶段，Rosetta为了更方便使用，在实现标准定义的基础上扩展了生命周期
- created：组件对象已经创建，有完整的接口，但是没有生成dom
- ready：dom已经生成，但是并未渲染到document上
- attached：已经渲染到document上
- attributechanged：属性更新了，触发条件是调用Rosetta element实例的update接口
- destroyed：组件销毁的接口，移除dom元素，解绑事件


### host的理解和使用
:host是为在css设置shadow root的样式，编译阶段会处理为此element类型的class


### 声明JS的依赖
在```<element></element>```中使用```<script type="text/javascript" src="xxx.js"></script>```引入其他JS依赖

```
<template>
    <script type="text/javascript" src="xxx.js"></script>
    <r-aaa>
        这是一个组件定义时使用其他自定义组件的例子
    </r-aaa>
</template>

```

### 声明三方组件依赖
在```<template></template>```中使用，```<link rel="import" type="text/html" href="r-aaa.html">```，来表示当前组件依赖的其他自定义组件

```
<template>
    <link rel="import" type="text/html" href="r-aaa.html">
    <r-aaa>
        这是一个组件定义时使用其他自定义组件的例子
    </r-aaa>
</template>
```
