### symbol 类型

#### 声明定义

```js
// 使值永远都是唯一
let sy1 = Symbol()
let sy2 = Symbol()
console.log(sy1 == sy2)

let sy3 = Symbol('描述')
console.log(sy3) //Symbol(描述)
console.log(sy3.description) //描述

// for定义相同的描述会使用同一个(可重复)
// for定义会在全局声明
let sy4 = Symbol.for('for')
console.log(Symbol.keyFor(sy4))
```

#### symbol 使用

```js
let user1 = '张三'
let user2 = '李四'
// 如果两个名字相同，就会出现覆盖的情况
user1 = {
	name: '张三',
	id: Symbol()
}
user2 = {
	name: '张三',
	id: Symbol()
}
let grade = {
	[user1.id]: { js: 100, css: 88 },
	[user2.id]: { js: 99, css: 77 }
}
console.log(grade[user2.id])
```

#### 扩展特性与对象属性保护

```js
let sym = Symbol('sanm')
let obj = {
	name: 'sanm',
	[sym]: 'sanm-zh'
}
// 普通遍历不会遍历出symbol属性

// 只会遍历出symbol属性
for (const key of Object.getOwnPropertySymbols(obj)) {
	console.log(key)
}
// 遍历所有属性
for (const key of Reflect.ownKeys(obj)) {
	console.log(key)
}
```
