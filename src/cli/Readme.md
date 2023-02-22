# 使用命令行

在使用`jest`的时候，我们常常会使用到命令行的方式运行测试，这可以给予我们一定的自由度来控制测试的运行。

## 方式

在命令行中使用`jest`有几种方式，其一就是直接使用已安装的本地`jest`，使用方式如下：
```shell
./node_modules/bin/jest --可选参数
```
其二是使用全局安装的`jest`脚本，使用方法如下：
```shell
jest --可选参数
```
其三是使用`pnpm`,`npm`和`yarn`这样的包管理器运行。这里以`pnpm`为例。在使用这种方式的时候，我们通常需要在`package.json`中添加一个脚本命令，如：
```json
{
  "script": {
    "test": "jest"
  }
}
```
当我们使用这样的方式来运行`jest`的时候，命令行要用以下的方式：
```shell
pnpm test -- --参数
```

## 具体参数

### --json

以`JSON`的形式输出测试结果

### --lastCommit

运行上一次`commit`中的所有测试

### --onlyChanged

只运行当前仓库中修改文件的测试。别名:`-o`

> 注意：这个命令只有在项目启用了`git`或`hg`仓库时才有用

### --silent

静默运行测试，不在控制台打印测试信息

### --bail[=<n>]

当失败的测试套件达到指定个数的时候，立即退出。默认时为`1`。别名：`-b`。

### --changedSince

只运行提供的`commit hash`或`分支`后的修改。

### --coverage[=<boolean>]

指定是否要测试代码覆盖率。别名：`--collectCoverage`

### --coverageDirector=<path>

指定代码覆盖率输出的目录

### --coverageProvider=<provider>

指定使用哪个选项来检测代码的覆盖率。可选项有`babel`和`v8`。默认为`babel`。

### --debug

使用调试样式运行`Jest`

### --env=<enviroment>

指定`Jest`运行的测试环境。可以指定任意的文件或node模块。如`jsdom`,`node`或`path/to/my-envoriment.js`.

### --expand

用于显示测试失败时详细的区别，而不是使用部分区别。别名：`-e`

### --init

以会话的形式初始化一个`jest.config.js`的配置文件。

### --listTests

列表检测到的所有测试


### --noStackTrace

在输出中，忽略堆栈追踪

### --passWithNoTests

当`Jest`检测到一个测试文件内没有任何测试时，将其标记为通过。

> 默认情况下，当一个测试文件内不包含测试时，会默认测试失败。

### --showConfig

显示Jest的配置内容


