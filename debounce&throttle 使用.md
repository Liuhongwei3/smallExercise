## lodash debounce
> [_.debounce](https://www.lodashjs.com/docs/lodash.debounce)
> [_.throttle](https://www.lodashjs.com/docs/lodash.throttle)

### 概念解释
[Debouncing and Throttling Explained Through Examples](https://css-tricks.com/debouncing-throttling-explained-examples/)

简洁版：
- debounce 防抖：某一时间范围内某个函数触发执行 n 次，但是只执行最后一次（也可只执行第一次），可设置 delay 时间延迟执行
- throttle 节流：某一时间范围内某个函数触发执行 n 次，但是在每隔 time 秒内最多执行一次，也可设置 delay 时间延迟执行

### 使用场景
- 防抖：持续点击按钮会触发 n 次 onClick，但是只需要执行一次，比如点击按钮然后请求数据
- 节流：持续输入关键词触发 n 次 onChange，但是只需要每隔一秒去请求一次搜索结果

### hooks 版本
由于在 react hooks 中每次页面更新时可能会使得未利用 useCallback 包裹的函数重新初始化，使得 setTimeout 的 timer 重置，从而 debounce 效果失效，不过可以通过 useRef + useCallback 来进行缓存实现。
具体详见：[hooks 中使用 debounce](https://www.jianshu.com/p/25c2509b3e6c)

### 细节注意
默认不能直接获取 debounce 和 throttle 包裹的函数的返回值，如若需要则应该传入回调函数的方式进行获取。
详见：[js中防抖、节流函数如何获取原函数的返回值？](https://segmentfault.com/q/1010000039894940)

### 业务落地
#### 背景
商品列表页请求商品数据的方法放置于 mobx reaction 中，会在请求条件变化时自动触发请求来更新列表数据，不过在页面切换行业线时存在多个请求状态变化（比如行业线、库节点、文件夹数据等），从而触发多次更新；

#### 解法
可在 store 中将 updateBrandgoods 方法使用 debounce 进行包裹，使得在多个请求状态变化时只会执行最后一次变化的请求状态

#### 不足
会出现上述 hooks 版本的问题，目前暂未处理，最合理的处理应该是页面初始化和 reaction 触发只需要执行最后一次
