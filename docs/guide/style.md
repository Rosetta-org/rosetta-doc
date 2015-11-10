## 默认样式和覆盖
Rosetta不为组件提供css的shadow功能

### 设置host的CSS
- 使用伪类选择器:host作为根节点的选择器
- 支持less、sass这类预处理程序

```
<element name="r-slider">
    <style>
        :host div {
            color: red;
        }
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
                text: {
                    type: String,
                    value: '测试'
                }
            }
        })
    </script>
</element>
```



### 声明CSS外链依赖
```
<element name="r-a">
    <style>
        :host div {
            color: red;
        }
    </style>
    <template>
        <link rel="stylesheet" type="text/css" href="a.css">
        <div>
            {text}
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-a',
            properties: {
                text: {
                    type: String,
                    value: '测试'
                }
            }
        })
    </script>
</element>
```

### css预处理程序
- 支持预处理程序
- style上需要标识出所用的预处理程序，```type="text/x-less"```或者```type="text/x-sass"```

```
<element name="r-a">
    <style type="text/x-less">
        :host {
            div {
                color: green;

                span {
                    color: red;
                }
            }
        }
    </style>
    <template>
        <link rel="stylesheet" type="text/css" href="a.css">
        <div>
            测试一下
            <span>
                {text}
            </span>
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-a',
            properties: {
                text: {
                    type: String,
                    value: '测试'
                }
            }
        })
    </script>
</element>
```
