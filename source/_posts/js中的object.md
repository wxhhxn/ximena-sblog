---
title: js中的object
date: 2021-09-26 17:03:55
tags: summary
categories: JS
---

# object:

对象的属性键只能是字符串类型或者 Symbol 类型

## ①symbol

Symbol 属性不参与 `for..in` 循环。

```javascript
let id = Symbol("id");
let user = {
  name: "John",
  age: 30,
  [id]: 123
};

for (let key in user) alert(key); // name, age (no symbols)

// 使用 Symbol 任务直接访问
alert( "Direct: " + user[id] );
```

## ②tostring/value

默认情况下，普通对象具有 `toString` 和 `valueOf` 方法：

- `toString` 方法返回一个字符串 `"[object Object]"`。
- `valueOf` 方法返回对象自身。

## ③对象引用和复制

```javascript
let user = {
  name: "John"
};
let user = { name: "John" };

let admin = user; // 复制引用
```

**赋值了对象的变量存储的不是对象本身，而是该对象“在内存中的地址”，换句话说就是对该对象的“引用”。**

对象的比较问题：两个对象为同一对象时，两者才相等。

所以可以通过引用来使两个值相同，也可以通过引用来修改对象的值

## ④对象的拷贝

```javascript
let user = {
  name: "John",
  age: 30
};

let clone = {}; // 新的空对象

// 将 user 中所有的属性拷贝到其中
for (let key in user) {
  clone[key] = user[key];
}
```

利用一个for循环将对象中所有的量加到clone对象中，修改clone对象中的值不改变原来的对象里面存储的值

也可以利用Object.assign来进行拷贝

```javascript
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// 将 permissions1 和 permissions2 中的所有属性都拷贝到 user 中
Object.assign(user, permissions1, permissions2);

// 现在 user = { name: "John", canView: true, canEdit: true }
```

**几个规则**

如果被拷贝的属性的属性名已经存在，那么它会被覆盖：

```javascript
let user = { name: "John" };

Object.assign(user, { name: "Pete" });

alert(user.name); // 现在 user = { name: "Pete" }
```

直接赋值给一个临时的空对象，然后赋值给clone

```javascript
let clone = Object.assign({}, user);
```

## ⑤构造器和操作符 "new"

在一个函数内部，我们可以使用 `new.target` 属性来检查它是否被使用 `new` 进行调用了。

对于常规调用，它为空，对于使用 `new` 的调用，则等于该函数：（利用这个来调试，就很方便）

```javascript
function User() {
  alert(new.target);
}

// 不带 "new"：
User(); // undefined

// 带 "new"：
new User(); // function User { ... }
```

⑥可选链

利用可选链依次对整条路径上的属性使用与运算进行判断，以确保所有节点是存在的（如果不存在，则停止计算）

```javascript
let user = {}; // user 没有 address 属性

alert( user?.address?.street ); // undefined（不报错）
```

```javascript
let user = null;
let x = 0;

user?.sayHi(x++); // 没有 "sayHi"，因此代码执行没有触达 x++

alert(x); // 0，值没有增加
```

1. `obj?.prop` —— 如果 `obj` 存在则返回 `obj.prop`，否则返回 `undefined`。
2. `obj?.[prop]` —— 如果 `obj` 存在则返回 `obj[prop]`，否则返回 `undefined`。
3. `obj.method?.()` —— 如果 `obj.method` 存在则调用 `obj.method()`，否则返回 `undefined`。
