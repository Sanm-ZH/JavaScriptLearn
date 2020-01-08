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

---

#### 语法

> [element0, element1, ..., elementN]
> new Array(element0, element1[, ...[, elementN]])
> new Array(arrayLength)

##### 参数

- **elementN**
  Array 构造器会根据给定的元素创建一个 JavaScript 数组，但是当仅有一个参数且为数字时除外（详见下面的 `arrayLength` 参数）。注意，后面这种情况仅适用于用 `Array` 构造器创建数组，而不适用于用方括号创建的数组字面量。
- **arrayLength**
  一个范围在 0 到 232-1 之间的整数，此时将返回一个 length 的值等于 `arrayLength` 的数组对象（言外之意就是该数组此时并没有包含任何实际的元素，不能理所当然地认为它包含 `arrayLength` 个值为 `undefined` 的元素）。如果传入的参数不是有效值，则会抛出 `RangeError` 异常。

---

#### 描述

数组是一种类列表对象，它的原型中提供了遍历和修改元素的相关操作。JavaScript 数组的长度和元素类型都是非固定的。因为数组的长度可随时改变，并且其数据在内存中也可以不连续，所以 JavaScript 数组不一定是密集型的，这取决于它的使用方式。一般来说，数组的这些特性会给使用带来方便，但如果这些特性不适用于你的特定使用场景的话，可以考虑使用类型数组 `TypedArray`。

只能用整数作为数组元素的索引，而不能用字符串。后者称为关联数组。使用非整数并通过方括号或点号来访问或设置数组元素时，所操作的并不是数组列表中的元素，而是数组对象的属性集合上的变量。数组对象的属性和数组元素列表是分开存储的，并且数组的遍历和修改操作也不能作用于这些命名属性。

**访问数组元素**

JavaScript 数组的索引是从 0 开始的，第一个元素的索引为 0，最后一个元素的索引等于该数组的长度减 1。如果指定的索引是一个无效值，JavaScript 数组并不会报错，而是会返回 `undefined`。

```js
var arr = [
	'this is the first element',
	'this is the second element',
	'this is the last element'
]
console.log(arr[0]) // 打印 'this is the first element'
console.log(arr[1]) // 打印 'this is the second element'
console.log(arr[arr.length - 1]) // 打印 'this is the last element'
```

虽然数组元素可以看做是数组对象的属性，就像 `toString` 一样，但是下面的写法是错误的，运行时会抛出 `SyntaxError` 异常，而原因则是使用了非法的属性名：

```js
console.log(arr.0); // a syntax error
```

并不是 JavaScript 数组有什么特殊之处，而是因为在 JavaScript 中，以数字开头的属性不能用点号引用，必须用方括号。比如，如果一个对象有一个名为 `3d` 的属性，那么只能用方括号来引用它。下面是具体的例子：

```js
var years = [1950, 1960, 1970, 1980, 1990, 2000, 2010];
console.log(years.0);   // 语法错误
console.log(years[0]);  // √
renderer.3d.setTexture(model, 'character.png');     // 语法错误
renderer['3d'].setTexture(model, 'character.png');  // √
```

注意在 3d 那个例子中，引号是必须的。你也可以将数组的索引用引号引起来，比如 `years[2]` 可以写成 `years['2']`。 `years[2]` 中的 2 会被 JavaScript 解释器通过调用 toString 隐式转换成字符串。正因为这样，`'2'` 和 `'02'` 在 `years` 中所引用的可能是不同位置上的元素。而下面这个例子也可能会打印 `true：`

```js
console.log(years['2'] != years['02'])
```

类似地，如果对象的属性名称是保留字（最好不要这么做！），那么就只能通过字符串的形式用方括号来访问（从 firefox 40.0a2 开始也支持用点号访问了）：

```js
var promise = {
	var: 'text',
	array: [1, 2, 3, 4]
}

console.log(promise['var'])
```

**length 和数字下标之间的关系**

JavaScript 数组的 `length` 属性和其数字下标之间有着紧密的联系。数组内置的几个方法（例如 `join`、`slice`、`indexOf` 等）都会考虑 `length` 的值。另外还有一些方法（例如 `push`、`splice` 等）还会改变 `length` 的值。

```js
var fruits = []
fruits.push('banana', 'apple', 'peach')

console.log(fruits.length) // 3
```

使用一个合法的下标为数组元素赋值，并且该下标超出了当前数组的大小的时候，解释器会同时修改 `length` 的值：

```js
fruits[5] = 'mango'
console.log(fruits[5]) // 'mango'
console.log(Object.keys(fruits)) // ['0', '1', '2', '5']
console.log(fruits.length) // 6
```

也可以显式地给 `length` 赋一个更大的值：

```js
fruits.length = 10
console.log(Object.keys(fruits)) // ['0', '1', '2', '5']
console.log(fruits.length) // 10
```

而为 `length` 赋一个更小的值则会删掉一部分元素：

```js
fruits.length = 2
console.log(Object.keys(fruits)) // ['0', '1']
console.log(fruits.length) // 2
```

这一节的内容在 `Array.length` 中有更详细的介绍。

**正则匹配结果所返回的数组**

使用正则表达式匹配字符串可以得到一个数组。这个数组中包含本次匹配的相关信息和匹配结果。`RegExp.exec`、`String.match`、`String.replace` 都会返回这样的数组。看下面的例子和例子下面的表格：

```js
// 匹配1个 d 后面紧跟着至少1个 b，再后面又跟着1个 d 的子串，
// 并且需要记住子串中匹配到的 b 和最后的 d （通过正则表达式中的分组），
// 同时在匹配时忽略大小写

myRe = /d(b+)(d)/i
myArray = myRe.exec('cdbBdbsbz')
```

该正则匹配返回的数组包含以下属性和元素：

| 属性/元素   | 说明                                                                                       | 示例              |
| ----------- | ------------------------------------------------------------------------------------------ | ----------------- |
| input       | 只读属性，原始字符串                                                                       | cdbBdbsbz         |
| index       | 只读属性，匹配到的子串在原始字符串中的索引                                                 | 1                 |
| [0]         | 只读元素，本次匹配到的子串                                                                 | dbBd              |
| [1], ...[n] | 只读元素，正则表达式中所指定的分组所匹配到的子串，其数量由正则中的分组数量决定，无最大上限 | [1]: bB<br>[2]: d |

---

#### 属性

- `Array.length`
  `Array` 构造函数的 length 属性，其值为 1（注意该属性为静态属性，不是数组实例的 length 属性）。
- `get Array[@@species]`
  返回 `Array` 构造函数。
- `Array.prototype`
  通过数组的原型对象可以为所有数组对象添加属性。

---

#### 方法

- `Array.from()`
  从类数组对象或者可迭代对象中创建一个新的数组实例。
- `Array.isArray()`
  用来判断某个变量是否是一个数组对象。
- `Array.of()`
  根据一组参数来创建新的数组实例，支持任意的参数数量和类型。

---

#### 数组实例

所有数组实例都会从 `Array.prototype` 继承属性和方法。修改 Array 的原型会影响到所有的数组实例。

##### 属性

- `Array.prototype.constructor`
  所有的数组实例都继承了这个属性，它的值就是 Array，表明了所有的数组都是由 `Array` 构造出来的。
- `Array.prototype.length`
  上面说了，因为 `Array.prototype` 也是个数组，所以它也有 length 属性，这个值为 0，因为它是个空数组。
