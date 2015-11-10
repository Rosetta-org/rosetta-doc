## 数据接口和properties
封装自定义组件需要定义清晰组件的接口，包括功能接口和初始化设置。Rosetta通过properties声明


### properties和attribute的映射规则
- 定义组件的时候声明properties属性的内容
- 页面初始化组件生成的时候，attribute传入的在properties中定义的值是有效初始化参数，建立一对一的关系


### 默认properties和attribute值
- 定义组件的时候声明properties属性的内容，如下例定义了'list'和'text'两个properties
```html
<element name="r-slider">
    <style>
    </style>
    <template>
        <div>
            {text}
        </div>
    </template>
    <script type="text/javascript">
        Rosetta({
            is: 'r-slider',
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
            }
        })
    </script>
</element>
```
- 以标签的方式使用组件时，设置attributes作为定义时的properties的初始化值
```
    <!DOCTYPE html>
    <html>
    <head>
        <title></title>
    </head>
    <body>
        <r-slider list="[{'title': 'init', 'src': 'http://www.baidu.com'}]">
    </r-slider>
    </body>
    </html>
```

### properties更新接口
```
    rosettaElementObj1.update({
        list: [
            {
                title: '更新数据',
                src: 'http://www.baidu.com'
            }
        ]
    })
```
