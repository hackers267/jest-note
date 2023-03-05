# 基本类型断言

基本类型断言匹配器有以下几个：

* [toBe](#tobe)
* [toBeEqual](#toequal)
* [toBeDefined](#tobedefined)
* [toBeTruthy](#tobetruthy)
* [toBeFalsy](#tobefalsy)
* [toBeNaN](#tobenan)
* [toBeNull](#tobenull)
* [toBeCloseTo](#tobecloseto)
* [toBeUndefined](#tobeundefined)

## toBe

*toBe*匹配器在`Jest`中的主要作用是用于断言基本类型的。其使用`Object.is`来判断断言结果，而不是使用的全等运算符(===)。

使用*toBe*
判断对象是否相等的时候，其判断是的两个对象是不是使用的同一个引用，而不是比较其字面值是否相等，如果要比较再个对象的字面量是否相等，请使用[toEqual](#toequal)。

请不要使用*toBe*来比较两个浮点数是否相等，因为实现的原因，在`JavaScript`和其它大多数的语言中，*0.1+0.2*并不完全等于*0.3*。(
因为精度丢失)。如果要比较两个浮点数，请使用[toBeCloseTo](#tobecloseto)。

> 注意：`Object.is`和全等运行符在`+0`和`-0`，`Number.NaN`和`NaN`
> 的运算上是不一样的。其他时候的运算结果是一致的。区别如图:![Object.is vs ===](Object_is_vs_===.png)

## toEqual

`toEqual`方法在处理基础类型上和`toBe`的行为是一致的。但在处理复杂类型(*对象*,*数组*,*Set*,*Map*等)时，`toBe`
是直接比较左右两边是否指向同一个引用。而`toEqual`则会对这些复杂类型进行递归调用`toEqual`方法，最终判断是字面量是否相等。如：

```ts
test("toEqual example", () => {
    const a = {
        id: 1,
        lang: 'JS'
    };
    const b = {
        id: 1,
        lang: 'JS'
    };
    expect(a).toEqual(b);
    expect(a).not.toBe(b);
})
```

## toBeDefined

## toBeTruthy

## toBeFalsy

## toBeNaN

## toBeNull

## toBeCloseTo

*toBeCloseTo*
用于判定两个给定的浮点数在指定的精度下是否相等。之所以需要指定精度，是因为在计算机的底层使用的是二进制表示的十进制的数字。并不是每一个十进制小数都可以使用二进制精确的表示，这就会丢失精度。所以才有了在指定精度下判断相等的方法。

*toBeCloseTo*的签名为`toBeCloseTo(number, numDigits?)`:

* `numDigits`为精度，可选，其默认值为*2*.其表示`Math.abs(expected - received) < 0.005`。其中，`0.005`和`2`
  的关系是：`(10**-2)/2`。

示例代码如下：

```ts
test('assert 0.1+0.2 and 0.3', () => {
    expect(0.1 + 0.2).toBeCloseTo(0.3, 5)
})
```

## toBeUndefined

## toBeGreaterThan

## toBeGreaterThanOrEqual

## toBeLessThan

## toBeLessThanOrEqual
