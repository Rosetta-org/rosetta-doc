## 为什么要有Rosetta
- 前端各种组件很多，但是组件复用度低是普遍存在的问题
- 已有的开发框架尤其是移动端的SPA解决方案，对于新人来说比较复杂，入门比较困难，影响开发效率
- 实现一种更直观、更容易入门的开发方式，同时兼顾性能、业务需求以及行业标准，以解决当前的开发效率问题

### Rosetta是什么？
- 一种实现声明式组件开发的前端库，让开发者能以标签形式使用组件，提升开发效率
- 以Web Components为标准，解决各类浏览器兼容性问题，尤其是移动端浏览器
- Custom Elements作为组件开发、使用规则；部分提供Shadow Dom功能；用HTML Imports引入组件、声明组件依赖关系；支持生命周期和数据动态更新
- 同时提供类似于DOM操作的动态接口，满足实际中的复杂开发情景需求

### 为开发提供四个级别的支持
- 组件开发
- 脚手架
- 项目构建
- 解决方案

### 用Custom Elements增强Web功能
HTML为开发者提供了一系列的原生元素比如``` <p>、<form>、<table>```，这类element有标准接口，比如attributes、properties、events以及默认样式。
开发者很熟悉用html元素来构建web页面，可惜这些标签数量和功能有限。如果要编写简单的轮播图等需要开发者写完整的html、css、javascript，并且处理静态资源管理和模块目录等问题。
通过custom elements我们可以扩展html的元素，这些标签可以有复杂的交互、精美的样式，但是依然能简单的使用。

```html
<r-tabs>
    <r-tab>
        第一个tab
    </r-tab>
    <r-tab>
        第二个tab
    </r-tab>
    <r-panel>
        第一个panel
    </r-panel>
    <r-panel>
        第二个panel
        <r-slider list="[]">
            <li>
                第一个slider
            </li>
            <li>
                第二个slider
            </li>
            <li>
                第三个slider
            </li>
        </r-slider>
    </r-panel>
</r-tabs>
```

### Rosetta与web components、Polymer的关系和差别？
- VS Web components：Web components标准提供了一系列新的接口，支持Web components的浏览器中支持用户自定义element，但是兼容性问题很大，参考[CaniUse](http://caniuse.com/#search=web%20components)
- VS Polymer：Polymer在运行时进行element解析对于性能有一定影响，而且对于浏览器尤其是手机的支持度不够产品级，比如在UC上无法正常使用
- Rosetta提供一系列custom elements方便开发者使用，提供动态接口支持运行时的Native的组件替换
- 一张图看清Rosetta


### 获取核心Rosetta elements


### 开始使用Rosetta！
如果对于Rosetta的声明式组件开发方式吸引，可以尝试

[手把手教你写一个helloworld](./helloworld.md)，（需要先[安装环境依赖](./beginning/install.md)哦）

或者，你是熟练的开发者，你可以访问

[初级使用](./lv1.md)

