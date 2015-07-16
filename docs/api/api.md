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

> 方法

- ref
- on
- off
- destroy

> 模版

- {} + js + jsx
- on-eventName || onEventName



### 创建element实例

- Rosetta.create
- Rosetta.render
- Rosetta.element(type, {
                            attr: attr,
                            children: children
                        }, target, ifReplace)


### 查找element实例
- Rosetta.ref


### 页面element完成渲染
- Rosetta.ready


### 触发页面级别的渲染
- Rosetta.init


### 异步加载
- Rosetta.import
