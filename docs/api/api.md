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
- on-eventName || onEventName



### 创建element实例

- Rosetta.create
- Rosetta.render，参数为空的时候默认进行页面custom element的初始化


### 查找element实例
- Rosetta.ref


### 页面element完成渲染
- Rosetta.ready


### 触发页面级别的渲染
- Rosetta.init => render


### 异步加载
- Rosetta.import


说明：
- 编译生成Rosetta.config，类似于
{
    'r-a.html': {
        elementName: 'r-a'
        url: 'r-a_xxx.js'
        deps: [r-b.html, r-c.html]
    },
    xxx
}

麻烦学芝补充详细结构

- 打包策略
    - 异步r-a依赖同步r-b，则r-a打包入r-b
    - 通过查config表获取类型，查是否注册过，注册过则不再异步加载
    - 异步r-a如果还依赖r-c，则走上一条策略判断是否需要异步加载

- 异步返回后，自动进行页面级的Rosetta.render

- SPA情况下，用户在更新页面dom后，主动调用Rosetta.render，来进行组件渲染



