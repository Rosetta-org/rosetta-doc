## 功能函数
Rosetta提供静态函数和element实例函数两级别接口

### element实例的函数/对象

- this.$[domRef]，传入dom的attribute定义的ref值
- this.on(eventName)，对Rosetta组件对象进行事件绑定
- this.off(eventName)，对Rosetta组件对象进行事件解绑
- this.query(selectorName)，查询内部dom节点的接口
- this.destroy()，销毁本Rosetta组件对象
- this.update(attributeObj)，更新组件properties



### 静态函数

- Rosetta.create(type, attributes, children)。创建Rosetta对象，此函数需要和render一起使用
- Rosetta.render(Rosetta.create(xxx), parentDOM, ifReplaceParent),
- Rosetta.ref('ref name')
- Rosetta({
        is: elementName,
        properties: {},
        attached: function(){},
        xxx
    })。组件定义接口，传入的参数将成为'is'定义的组件名的这类组件的prototype
- Rosetta.ready(function)。页面上组件完全渲染完毕就执行参数传入的callback