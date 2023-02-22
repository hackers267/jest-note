# 测试异步函数

在`Jest`中测试异步函数主要有4种方法：

* 在`test`中返回的`Promise`中断言
* 使用`async`和`await`
* 在回调函数中使用`done`函数
* 使用`resolves`和`rejects`

## 返回`Promise`

如果要测试的函数返回的是一个`Promise`，那么我们就可以让`test`返回`Promise`，在`Promise`中使用断言。比如：

```js
test('the data is peanut butter', () => {
    return fetchData().then(data => {
        expect(data).toBe('peanut butter');
    })
})
```

这样，我们就可以测试这个`Promise`函数了。

> 注意：我们一定要返回`Promise`，让`Jest`知道这是一个异步函数，在`Promise`的`resolve`
> 后进行断言，否则，Jest会提前断言。这个时候，`Promise`的状态还没有改变，得不到我们想要的结果。如果`Promise`没有`resolve`
> ，而是`jest`了，那么测试会直接失败。

## `async`/`await`

在测试异步代码的时候，我们可以直接使用`async`和`await`。就像下面一样：

```js
test('the data is peanut butter', async () => {
    const data = await fetchData();
    expect(data).toBe('peanut butter');
})

test('the fetch fails with an error', async () => {
    expect.assertions(1);
    try {
        await fetchData();
    } catch (e) {
        expect(e).toMatch('error');
    }
})
```

在使用`async`/`await`测试异步代码的时候，我们要给`test`函数添加`async`标记，在异步代码前使用`await`。

当使用`async`/`await`测试异步代码失败的时候，记得一定要使用`assertions`来断言测试有过断言，否则测试不能通过。

## 使用回调函数

如果我们要测试的异步代码是在回调函数中，而不是在`Promise`里，那么我们就需要使用`test`函数中单参数`done`来解决问题了。比如：

```js
test('the data is peanut butter', done => {
    function callback(error, data) {
        if (error) {
            done(error);
            return;
        }
        try {
            expect(data).toBe('peanut butter');
            done();
        } catch (error) {
            done(error);
        }
    }

    fetchData(callback);
})
```

在这个例子中，如果`done()`函数从来没有执行过，那么测试会超时失败。

如果`expect`执行失败，那么其将抛出一个错误，其后的`done`
就不会执行。如果我们想要知道具体为什么会失败，那么我们就要在测试中捕获这个错误。所以需要把`expect`放入`try`中，然后在`catch`
中捕获错误，使用`done`来接收`error`的值。

## 使用`resolves`和`rejects`

我们也可以让`test`中的函数返回一个`resolves`或`rejects`来测试异步代码。比如：

```js
test('the data is peanut butter', () => {
    return expect(fetchData()).resolves().toBe('peanut butter');
})
```

直接通过`resolves`来声明我们期望`Promise`的状态会变为`resolve`状态，并返回`peanut butter`，否则测试失败（无论`Promise`
是变为`reject`还是`resolve`后返回的不是`peanut butter`）。

同理，通过`rejects`,我们期望`Promise`的状态会变为`rejects`，并返回一个指定的错误。如：

```js
test('the fetch fails with an error', () => {
    return expect(fetchData()).rejects.toMatch('error');
})
```

## 测试RxJs中`Promise`的行为

因为`RxJs`的实现机制和`Promise`微任务的问题，在`RxJs`中不能使用弹珠测试，那么我们就要使用`Jest`中测试异步代码中的方法来解决问题了。比如：

```js
// Some RxJS code that also consumes a Promise, so TestScheduler won't be able
// to correctly virtualize and the test will always be really asynchronous.
const myAsyncCode = () => from(Promise.resolve('something'));

it('has async code', (done) => {
    myAsyncCode().subscribe((d) => {
        assertEqual(d, 'something');
        done();
    });
});
```
