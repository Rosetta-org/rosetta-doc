## 脚手架

在手动使用

为了大家可以快速体验和使用Rosetta，我们提供了快速启动项目的脚手架

只需<font color="red">三行</font>命令便可快速使用Rosetta


- 初始化脚手架
``` js
    mkdir demo
    cd demo
    fis3 init rosetta
```

- 运行和预览
``` js
    fis3 server start --type node
    fis3 release -w
```

- 自动生成新的element脚手架
```js
    fis3 init element
```

- 指定目录获得产出产品代码
```js
    fis3 release production -d ./output
```


- 查看编译报错
```js
    fis3 release -w --verbose
```


- 想查看更新信息，访问github上[脚手架源码](https://github.com/fis-scaffold/rosetta)