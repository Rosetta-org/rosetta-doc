## 事件

### 为内部DOM绑定事件
- 可以以attribute的形式，使用内置接口，为内部的dom绑定事件
- 可以自行使用你喜欢的方式绑定事件
- 使用attribute形式绑定事件，比如onClick={callback}，以驼峰格式进行声明

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
                console.log('click test');
            }
        })
    </script>
</element>
```



### 目前支持的事件（目前只包含原生事件）
- onClick
- onDoubleClick
- onDrag
- onDragEnd
- onDragEnter
- onDragExit
- onDragLeave
- onDragOver
- onDragStart
- onDrop
- onMouseDown
- onMouseEnter
- onMouseLeave
- onMouseMove
- onMouseOut
- onMouseOver
- onMouseUp


- onTouchStart
- onTouchEnd
- onTouchCancel
- onTouchMove


- onScroll
- onWheel


- onCopy
- onCut
- onPaste


- onKeyDown
- onKeyPress
- onKeyUp


- onFocus
- onBlur


- onChange
- onInput
- onSubmit


### 自定义事件的使用
- 除上述事件意外
