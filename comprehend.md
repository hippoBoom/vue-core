### vue 核心原理——Object.defineProperty

#### 语法

> Object.defineProperty(obj , prop , descriptor)

#### `参数`

##### `obj`

要修改的对象

##### `prop`

要定义或修改的属性名

##### `descriptor`

#### 属性描述符

对象里目前存在的属性描述符有**两种**主要形式：**数据描述符**和**存取描述符**。数据描述符是一个具有值的属性，该值可能是可写的，也可能不是可写的。存取描述符是由 getter-setter 函数对描述的属性。**描述符必须是这两种形式之一；不能同时是两者。**

**数据描述符**和**存取描述符**均具有以下可选键值：

##### `configurable`

当属性为 false 时，属性属性描述符无法修改，属性也无法在对象上被删除。**默认值为 false。**

##### `enumerable`

当前对象是否可以枚举。**默认值为 false。**

**数据描述符**具有以下可选键值：

##### `value`

该属性对应的值，**默认值为 undefined。**

##### `writable`

该属性是否可以被赋值，**默认值为 false。**

**存取描述符**具有以下可选键值：

##### `get`

一个给属性提供 getter 的方法，如果没有 getter 则为 undefined。当访问该属性时，该方法会被执行，方法执行时没有参数传入，但是会传入`this`对象（由于继承关系，这里的 this 并不一定是定义该属性的对象）。
**默认为 `undefined`。**

##### `set`

一个给属性提供 setter 的方法，如果没有 setter 则为 undefined。当属性值修改时，触发执行该方法。该方法将接受唯一参数，即该属性新的参数值。
**默认为 `undefined`。**

#### 事例

```js
var o = {}; // 创建一个新对象

// 在对象中添加一个属性与数据描述符的示例
Object.defineProperty(o, "a", {
  value: 37,
  writable: true,
  enumerable: true,
  configurable: true
});

// 对象o拥有了属性a，值为37

// 在对象中添加一个属性与存取描述符的示例
var bValue;
Object.defineProperty(o, "b", {
  get: function() {
    return bValue;
  },
  set: function(newValue) {
    bValue = newValue;
  },
  enumerable: true,
  configurable: true
});

o.b = 38;
// 对象o拥有了属性b，值为38

// o.b的值现在总是与bValue相同，除非重新定义o.b

// 数据描述符和存取描述符不能混合使用
Object.defineProperty(o, "conflict", {
  value: 0x9f91102,
  get: function() {
    return 0xdeadbeef;
  }
});
// throws a TypeError: value appears only in data descriptors, get appears only in accessor descriptors
```

# 有待补充
