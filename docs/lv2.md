## 高级使用
高级使用文档主要说明了Rosetta提供的动态特性
- 动态实例化element
- 异步加载注册element

### 动态实例化element
Rosetta为开发者提供声明式element使用方式，同时对标createElement、append接口，提供动态实例化element的函数

- Rosetta.create
    - 生成Rosetta element的Object
    - 返回Rosetta element的Object，可以作为第一个参数参数传递给Rosetta.render接口
    - 接口参数为(elementName, childrenArr)
    - elementName为注册的element名字
    - childrenArr为子元素数组，每一项是DOM或者Rosetta element的Object

- Rosetta.render
    - 将element的DOM渲染到target的DOM上
    - 接口参数为(elementObject, targetDOM, ifReplaceTarget)
    - targetDOM为element实例渲染的位置
    - ifReplaceTarget为true表示替换targetDOM，为false表示作为targetDOM的子元素

### 异步加载注册element
