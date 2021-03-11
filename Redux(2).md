# Redux 介绍（二）

1. compose

```typescript
  /**
   * 从右到左组合单参数函数，最右侧的函数可以使用多个参数，因为它为生成的复合函数提供了签名。
   * 
   * @param funcs The functions to compose.
   * @returns 通过从右到左组合参数函数获得的函数，例如 `compose(f, g, h)` 等同于 `(...args) => f(g(h(...args)))`。
   */
   export default function compose(...funcs: Function[]) {
    if (funcs.length === 0) {
      // infer the argument type so it is usable in inference down the line
      return <T>(arg: T) => arg
    }

    if (funcs.length === 1) {
      return funcs[0]
    }

    return funcs.reduce((a, b) => (...args: any) => a(b(...args)))
  }
```

2. pipe

```typescript
  /**
   * Array.reduce 功能性函数管道
   * 
   * @ param funcs The functions to call.
   * @return 通过从左到右执行参数函数，并将执行结果累计传入给下一个参数函数，例如 `pipe(f, g, h)` 等同于 `(...args) => h(g(f(...args))`。
   */
  const pipe = (...functions) => input => functions.reduce(
      (acc, fn) => fn(acc),
      input
  );
```
[点击这里查看示例](https://codesandbox.io/s/function-composition-enabling-pipe-u06ip)
