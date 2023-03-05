# 数组类断言

`Jest`中和数组相关的断言匹配器有下面一些：

* [toContain](#tocontain)
* [toContainEqual](#tocontainequal)
* [toHaveLength](#tohavelength)
* [expect.arrayContaining](#expectarraycontaining)

## toContain

`toContain`用于判断数组中是否包含指定的元素。其使用`===`来判断数组中的项目和给定内容的比较。比如:

```ts
const array = [1, 2, 3];
test('assert toContain', () => {
    expect(array).toContain(2);
})
```

`toContain`不仅仅用于数组，还可以用于其他可迭代类型，比如*字符串*,*集合*,*node集合*和*HTML集合*等。

> 注意，因为`toContain`中使用的是`===`。所以，如果数组中的项目是对象，那么比较的是对象的引用是否是同一个，而不是比较字面量。

## toContainEqual

`toContainEqual`同样是用于判断数组中是否包含指定的元素。其和`toContain`的区别在于，`toContain`
对于复杂类型的比较是比较其引用。而`toContainEqual`是比较其字面量。就和`toBe`和`toEqual`一样。
比如：

```ts
const array = [{id: 1}, {id: 2}];
test(`assert toContainEqual`, () => {
    expect(array).toContainEqual({id: 1})
})
```

## toHaveLength

`toHaveLength`用于检查一个数组中元素的个数或字符串的长度。比如：

```ts
test('assert toHaveLength', () => {
    expect([1, 2, 3]).toHaveLength(3);
})
```

> 注意，`toHaveLength`不仅仅可以用于数组和字符串，它可以用于任何有`length`属性的对象。用于判断其`length`是否等于指定的数值。
## expect.arrayContaining

`expect.arrayContaining(array)`可以用于判断一个数组是不是另一个数组的子数组。其主要需要配合`toEqual`或`toBeCalledWith`使用。还可以配合`objectContaining`或`toMatchObject`使用。

```ts
it('assert arrayContaining', function () {
    const expected = [1, 2, 3];
    expect([1, 2, 3, 4]).toEqual(expect.arrayContaining(expected));
}); 
```
