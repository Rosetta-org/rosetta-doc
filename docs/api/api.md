### API接口

### element类注册
> 属性

- is
- ready
- created
- attached
- dettached
- attributeChanged
- extends
- properties

说明
1、properties里的项优先级高于其他this.xxx
2、使用with
3、模版里用属性（变量）可以省略'this'以及'properties'

> 方法

- $ => 选ref属性
- on
- once
- off
- update
- destroy


> 模版

- {} + js + jsx
- onEventName



### 创建element实例

- Rosetta.create
- Rosetta.render，参数为空的时候默认进行页面custom element的初始化


### 查找element实例
- Rosetta.ref


### 页面element完成渲染
- Rosetta.ready


### 触发页面级别的渲染
- Rosetta.render


### 异步加载
- Rosetta.import





