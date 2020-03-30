# shop_vue

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

1.设置接口参数校验规则
方式1--------------
定义一个JSON格式
例如
validRules:[
    {

        field1:
        [
        { required: true, message: '缺少field1参数'},
        { min: 5, max:10,message: '长度必须满足5-10个字符'},
        { regex: '^\d{4}-\d{1,2}-\d{1,2}',message: '日期格式不正确'}
        ],
        field2:
        [
        { required: true, message: '缺少field2参数'},
        { min: 5, max:10,message: '长度必须满足5-10个字符'},
        { regex: '(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)',message: '身份证号格式不正确'}
        ],

    }

]

在调用接口时读取以上字段配置数据，遍历参数是否匹配以上规则，是就放行，否则异常

如果业务系统和代码生成器是相互分离的，专门写个接口为这些配置的字段JSON生成一个sql脚本，存入到数据库表中。
然后每个生成的接口都有这样一个函数去数据库读取数据并校验

方式2----------------
使用springboot的@valid注解中的@Pattern指定验证规则
代码则使用反射将前端配置的规则动态传递给注解
这个就复杂点



