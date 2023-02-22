# 全局对象 test

在`Jest`中，全局对象`test`有一个别名`it`，在也就是说，在`Jest`中能使用`test`的地方也可以使用`it`来替代。

## test

`test`对象最简单的使用如下：

```javascript
test('testName', () => {
    expect(1 + 1).toBe(2)
})
```

`test`函数接收三个参数。

* 第一个参数为测试方法的名称，通过这个名称可以在测试失败的时候，更加精确的定位是哪个测试失败了。
* 第二个参数是一个匿名函数。在这个函数中应该包含本测试的准备工作和一个或多个断言函数。(推荐只在一个`test`
  方法中包含一个断言函数，虽然`Jest`允许在`test`中包含多个断言函数)。
* 第三个参数(可选)是测试运行的超时时间，如果函数运行超时，则自动失败。默认是5s。

如果`test`第二个参数的函数返回一个`Promise`，那么，在`Promise`状态改变后，断言才会生产。比如`asyncBe`是返回一个`Promise`
。那么可以像这样测试：

```js
test("test the asyncBe", () => {
    return asyncBe(1).then(v => {
        expect(v).toBe(1)
    })
})
```

关于异步函数的测试，请参考[异步函数的测试](../async/Readme.md)

## test.only

`test.only`可以使`Jest`
只运行一个测试块中当前的测试。这在调试测试的时候会非常有用。它可以让你只运行当前的测试，而忽略其它测试，以此来提升测试速度和减少反馈时间。`test.only`
有一个别名：`fit`。

示例如下：

```js
test.only('it is raining', () => {
    expect(inchedOfRain()).toBeGreaterThan(0);
});

test('it is not snow', () => {
    expect(inchedOfSnow()).toBe(0);
});
```

在上面的示例中，当运行测试的时候，只会运行*it is raining*测试，因为其标记了`only`。

> 注意：请不要把`test.only`提交到仓库中，它应该只是你调试测试的一个常用工具。

## test.todo

`test.todo`用于指定计划添加测试的时候。其只接收一个参数，即**测试的名称**。使用`test.todo`
标记的测试会在最后的汇总的时候高亮，所以可以方便的知道还有哪些计划的测试需要添加。

> 注意：`test.todo`如果包含了函数会抛出错误。如果你已经有了一个实现测试的测试，但不想运行它。请使用`todo.skip`。

## test.skip

当正在维护一个很大的代码的时候，如果一个测试因为某些原因临时遭到了破坏。但又不想删除它。只想临时跳过这个测试。这个时候就可以使用`test.skip`。别名：`xit`,`xtest`。

示例如下：

```js
test('it is raining', () => {
    expect(inchesOfRain()).toBeGreaterThan(0)
});

test.skip('it is not snowing', () => {
    expect(inchesOfSnow()).toBe(0)
})
```

上面的代码只会运行*it is raining*。因为其使用了`test.skip`。

## test.concurrent

`test.concurrent`目前是一个实验性的功能。其作用是显式指定其测试开发运行。其包含的函数和`test`基本一致。只是第二个参数接收的是一个包含有断言的
**异步函数**.

示例：

```js
test.concurrent('addition of 2 numbers', async () => {
    expect(5 + 3).toBe(8);
});

test.concurrent('subtracting 2 numbers', async () => {
    expect(5 - 3).toBe(2);
})
```

> 注意：当在测试中使用了`test.concurrent`时，最配置`maxConcurrency`选项，用来防止`Jest`同时运行太多的测试。

 
