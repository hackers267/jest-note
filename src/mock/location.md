# location的mock

在开发浏览器应用的时候，我们会不可避免的使用到`window.location`对象(后面直接称为`location`对象)
。当我们的方法使用到`location`对象的时候，要对这个方法进行单元测试，那我们就需要使用方法来`mock`这个`location`对象。

下面是我们要mock`location`的方法和步骤：

## 安装依赖

我们需要知道的是，我们使用`location`的场景是在浏览器端，所以我们的测试环境也应该是和浏览器相关的。这里我们使用`jsdom`
环境。首先，我们需要安装依赖`jest-environment-jsdom`:

```shell
pnpm add -D jest-environment-jsdom
```

## 设置测试环境

设置测试环境的方法有两种，一种是在配置文件中指定全部测试的测试环境，一种是测试文件中单独指定测试文件自身的测试环境。我们这里使用第二种方法：

```ts
/**
 * @jest-environment jsdom
 */
```

## 设置mock方法

为了使用方法，我们可以提取一个公共的mock方法，如下：

```ts
function stubLocation(location: Record<string, any>) {
    jest.spyOn(window, "location", "get").mockReturnValue({
        ...window.location,
        ...location,
    });
}
```

之后，我们就可以直接在测试中调用`stubLocation`方法为`location`进行`mock`了。

## 总结

我们通过安装依赖，设置测试环境和添加公共的mock方法，实现了对`location`的包装。具体示例如下：

```shell
pnpm add -D jest-environment-jsdom
```

```ts
/**
 * @jest-environment jsdom
 */

test("test location", () => {
    stubLocation({url: "https://www.exmaple.com"});
    expect(localtion.url).toBe("https://www.example.com")
})

function stubLocation(location: Record<string, any>) {
    jest.spyOn(window, "location", "get").mockReturnValue({
        ...window.location,
        ...location,
    });
}

```
