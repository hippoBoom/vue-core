#### 扫盲区

`!!boolean`
!一个表示把任何数据类型转换为 Boolean 值两个!!就是没变

---

> 响应式原理（上）

##### `defineReactive`

把对象上的属性变成响应式的就方法

##### `shouldObserve`

标识符，符合会new 一个 Observer 一个实例

##### `toggleObserving`

改变 shouldObserve 状态

##### `dep`

**_尚未介绍_**

##### `def`

是对 Object.defineProperty 做了一个封装

##### `observer`

观测数据

问题`__ob__`属性是干嘛的？

```js
export function observe(value: any, asRootData: ?boolean): Observer | void {
  if (!isObject(value) || value instanceof VNode) {
    return;
  }
  let ob: Observer | void;
  //   判断value有没有__ob__属性并且是Object的实例
  if (hasOwn(value, "__ob__") && value.__ob__ instanceof Observer) {
    ob = value.__ob__;
  } else if (
    shouldObserve &&
    !isServerRendering() &&
    (Array.isArray(value) || isPlainObject(value)) &&
    Object.isExtensible(value) &&
    !value._isVue
  ) {
    ob = new Observer(value);
  }
  if (asRootData && ob) {
    ob.vmCount++;
  }
  return ob;
}
```
