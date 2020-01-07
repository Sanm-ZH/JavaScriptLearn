### 数组

JavaScript 的 Array 对象是用于构造数组的全局对象，数组是类似于列表的高阶对象。

##### 创建数组

```js
var fruits = ['Apple', 'Banana']

console.log(fruits.length)
// 2
```

##### 通过索引访问数组元素

```js
var first = fruits[0]
// Apple

var last = fruits[fruits.length - 1]
// Banana
```

##### 遍历数组

```js
fruits.forEach(function(item, index, array) {
	console.log(item, index)
})
// Apple 0
// Banana 1
```

##### 添加元素到数组的末尾

```js
var newLength = fruits.push('Orange')
// newLength:3; fruits: ["Apple", "Banana", "Orange"]
```

##### 删除数组末尾的元素

```js
var last = fruits.pop() // remove Orange (from the end)
// last: "Orange"; fruits: ["Apple", "Banana"];
```

##### 删除数组最前面（头部）的元素

```js
var first = fruits.shift() // remove Apple from the front
// first: "Apple"; fruits: ["Banana"];
```

##### 添加元素到数组的头部

```js
var newLength = fruits.unshift('Strawberry') // add to the front
// ["Strawberry", "Banana"];
```

##### 找出某个元素在数组中的索引

```js
fruits.push('Mango')
// ["Strawberry", "Banana", "Mango"]

var pos = fruits.indexOf('Banana')
// 1
```

##### 通过索引删除某个元素

```js
var removedItem = fruits.splice(pos, 1) // this is how to remove an item

// ["Strawberry", "Mango"]
```

##### 从一个索引位置删除多个元素

```js
var vegetables = ['Cabbage', 'Turnip', 'Radish', 'Carrot']
console.log(vegetables)
// ["Cabbage", "Turnip", "Radish", "Carrot"]

var pos = 1,
	n = 2

var removedItems = vegetables.splice(pos, n)
// this is how to remove items, n defines the number of items to be removed,
// from that position(pos) onward to the end of array.

console.log(vegetables)
// ["Cabbage", "Carrot"] (the original array is changed)

console.log(removedItems)
// ["Turnip", "Radish"]
```

### 复制一个数组

```js
var shallowCopy = fruits.slice() // this is how to make a copy
// ["Strawberry", "Mango"]
```
----
#### 语法
>[element0, element1, ..., elementN]
>new Array(element0, element1[, ...[, elementN]])
>new Array(arrayLength)
##### 参数
- **elementN**
Array 构造器会根据给定的元素创建一个 JavaScript 数组，但是当仅有一个参数且为数字时除外（详见下面的 `arrayLength` 参数）。注意，后面这种情况仅适用于用 `Array` 构造器创建数组，而不适用于用方括号创建的数组字面量。
- **arrayLength**
一个范围在 0 到 232-1 之间的整数，此时将返回一个 length 的值等于 `arrayLength` 的数组对象（言外之意就是该数组此时并没有包含任何实际的元素，不能理所当然地认为它包含 `arrayLength` 个值为 `undefined` 的元素）。如果传入的参数不是有效值，则会抛出 `RangeError` 异常。
----
#### 描述
数组是一种类列表对象，它的原型中提供了遍历和修改元素的相关操作。JavaScript 数组的长度和元素类型都是非固定的。因为数组的长度可随时改变，并且其数据在内存中也可以不连续，所以 JavaScript 数组不一定是密集型的，这取决于它的使用方式。一般来说，数组的这些特性会给使用带来方便，但如果这些特性不适用于你的特定使用场景的话，可以考虑使用类型数组 TypedArray。

只能用整数作为数组元素的索引，而不能用字符串。后者称为关联数组。使用非整数并通过方括号或点号来访问或设置数组元素时，所操作的并不是数组列表中的元素，而是数组对象的属性集合上的变量。数组对象的属性和数组元素列表是分开存储的，并且数组的遍历和修改操作也不能作用于这些命名属性。

**访问数组元素**

JavaScript 数组的索引是从0开始的，第一个元素的索引为0，最后一个元素的索引等于该数组的长度减1。如果指定的索引是一个无效值，JavaScript 数组并不会报错，而是会返回 `undefined`。

----
#### 属性
- `Array.length`
`Array` 构造函数的 length 属性，其值为1（注意该属性为静态属性，不是数组实例的 length 属性）。
- `get Array[@@species]`
返回 `Array` 构造函数。
- `Array.prototype`
通过数组的原型对象可以为所有数组对象添加属性。
----
#### 方法
- `Array.from()`
从类数组对象或者可迭代对象中创建一个新的数组实例。
- `Array.isArray()`
用来判断某个变量是否是一个数组对象。
- `Array.of()`
根据一组参数来创建新的数组实例，支持任意的参数数量和类型。
----
#### 数组实例
所有数组实例都会从 `Array.prototype` 继承属性和方法。修改 Array 的原型会影响到所有的数组实例。

##### 属性
- `Array.prototype.constructor`
所有的数组实例都继承了这个属性，它的值就是 Array，表明了所有的数组都是由 `Array` 构造出来的。
- `Array.prototype.length`
上面说了，因为 `Array.prototype` 也是个数组，所以它也有 length 属性，这个值为 0，因为它是个空数组。
