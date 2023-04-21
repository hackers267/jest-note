# Date

当使用JS编写代码的时候，常常需要使用`Date`对象来获取当前时间。因为`Date`是当前时间，我们使用和`Date`相关的方法的时候，就不好写测试。使用其是和时间有关的。
使用`jest`代码的时候，我们可以使用`jest.setSystemTime`来设置当前时间。

如下：
```javascript
it("test date", () => {
  jest.setSystemTime(new Date("2022-01-01"));
  const date = new Date();
  expect(date.getFullYear()).toBe(2022);
})

```
