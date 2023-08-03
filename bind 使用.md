## 示例

```js
let x = 1;

const addTwo = y => {
  console.log('cur y', y);

  return y + 2;
};

const func = () => {
  const xBind = addTwo.bind(null, x);

  console.log('pre cur x', x);
  console.log('pre xBind', xBind());
  console.log('addTow x1', addTwo(x));
  
  x += 3;

  console.log('cur x', x);
  console.log('xBind', xBind());
  console.log('addTow x2', addTwo(x));
}

func();

// pre cur x 1
// cur y 1
// pre xBind 3
// cur y 1
// addTow x1 3
// cur x 4
// cur y 1
// xBind 3
// cur y 4
// addTow x2 6
```

## 小结

- `bind` 函数在针对使用 `全局变量` 的时候可 `绑定当前值`，若不使用 Bind，则每次调用对应函数时使用的则是 `函数执行` 时全局变量的值。
- 具体应用例如 react hooks 源码中使用 bind 去绑定当前组件的 fiber ，示例见：[react hooks bind](https://github.com/facebook/react/blob/main/packages/react-reconciler/src/ReactFiberHooks.js#L1186)

