# Umi Jest

## Mock History

在`umi`中，`history`是命令行导航或说是路由的方式。我们可以通过像`history.push("/")`的方式进行路由跳转。当要给`history`添加单元测试的使用，我们可以使用下面的方式：

```typescript
import { history } from 'umi';
jest.mock("umi",()=>{
    return {
        history: {
            push: jest.fn()
        }
    }
})
describe('history', function () {
    it('should be /', function () {
        expect(history.push).toBeCalledWith("/");
    });
});
```
 这里的关键点在于：
1. 在当前测试中添加`history`的显示引入
2. 使用`toBeCalledWith`来判定`history`的push方法接收到的是我们预期的参数。
