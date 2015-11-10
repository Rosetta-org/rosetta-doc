## 数据绑定
这里描述了，如何编写动态模版、如何进行数据更新和触发UI渲染的机制。
模板语法以```{}```包裹jsx形式作为模板语法，以下是关于模板的几个方面


### 模版语法
目前支持的是jsx语法，点击[jsx](http://facebook.github.io/jsx/)了解更多关于jsx的信息

### 数据更新和UI渲染
更新操作统一通过update接口完成，调用rosetta组件对象实例的update接口，Rosetta将为你自动完成properties值的更新、UI的重新渲染

- 定义中调用update，内部函数可以通过this获取对象

```html
<element name="r-example">
    <style>
    </style>
    <template>
        <div onClick={clicktest}>
            {text}
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-example',
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
            },

            clicktest: function() {
                this.update({
                    text: '更新啦'
                });
            }
        })
    </script>
</element>
```


- 使用后调用update接口

```
    <!DOCTYPE html>
    <html>
    <head>
        <title></title>
    </head>
    <body>
        <r-example ref="example"></r-example>
        <script type="text/javascript">
            Rosetta.ready(function() {
                Rosetta.ref('example').update({
                    text: '外部更新一下'
                });
            });
        </script>
    </body>
    </html>
```