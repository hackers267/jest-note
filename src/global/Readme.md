# 全局对象

为了方便在测试中使用，`Jest`自动在测试文件中注入了全局对象`describe`,`test`和`expect`。通过自动注入的方式使得我们在测试文件中不再需要显示的重复`import {describe, expect, text} from '@jest/globals'`引用了。

`Jest`的全局对于可以分为以下几类：
* 钩子类
  * afterAll
  * beforeAll
  * afterEach
  * beforeEach
* describe类
* test类
* expect类

因为`expect`类比较重要，所以单独记录。
