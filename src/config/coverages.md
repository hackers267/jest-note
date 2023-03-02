# 代码覆盖率

当在测试中需要输出代码覆盖率的时候，我们需要进行一定的配置，下面是一个配置示例：

```js
module.exports = {
    collectCoverage: true,
    coverageThreshold: {
        global: {
            branches: 95,
            functions: 95,
            lines: 95,
            statements: 95
        },
        './src/reducers/**/*.ts': {
            statements: 90
        },
        './src/utils/**/*.ts': {
            functions: -5
        }
    },
    coverageDirectory: 'reports',
    collectCoverageFrom:["src/**/*.ts","!**/node_modules/**"],
    coveragePathIgnorePatterns: ["<rootDir>/dist/","<rootDir>/node_modules/"],
    coverageProvider: "babel",
    coverageReporters: ["clover","json",'lcov',['text',{skipFull: true}]]
}
```

在这个配置示例中，我们对其中的各个字段分别进行一下讲解：

* `collectCoverage`字段为一个boolean值，指定其为`true`时，才会触发代码覆盖率的收集操作
* `coverageThreshold`字段是对代码覆盖率的统计指标的定义。其可以定义一个全局的代码覆盖率的指标，用`global`表示，其中要求`branches(条件分支)`的覆盖率最少达到`95%`，`functions(函数)`的代码覆盖率最少也要达到`95%`，`lines代码行`的代码覆盖率也要达到`95%`,`statements(语句)`的代码覆盖率也要达到`95%`。此外，我们还可以单独指定某个匹配模式下对应的代码覆盖率，比如示例中`./src/reducers/**/*.ts`模式下`statements`的代码覆盖率达到`90%`即可。也可以指定一个负值，用于表示没有覆盖的测试的最大数量，比如示例中`./src/utils/**/*.ts`模式下，`functions`没有测试的最大数量为5。一旦测试的代码覆盖率达不到我们设置的指标，那么测试就会失败。
* `coverageDirectory`用于指定代码覆盖率输出报告的文件目录，如果没有设置这个属性，那么报告会输出到项目目录的`coverage`目录中。
* `collectCoverageFrom`用于指定从什么地方收集要测试的代码。
* `coveragePathIgnorePatterns`用于指定测试时，要忽略哪些目录下的代码。
* `coverageProvider`用于指定输出报告的提供者，可选的有`babel`和`v8`，默认使用`babel`。
* `coverageReporters`用于指定输出报告的格式。默认值为`["clover", "json", "lcov", "text"]`。

除了在示例中提及到的几个有关代码覆盖率的选项外，还有一个`forceCoverageMatch`选项，其主要用于从上面的配置中已忽略的部分再添加进测试中。

## 报告格式

[//]: # (todo：添加报告格式)
