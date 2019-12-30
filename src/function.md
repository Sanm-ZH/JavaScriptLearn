### 函数

#### 函数声明

```js
function test(str) {
	console.log(str)
}
test('sanm')

const user = {
	name: null,
	setUserName(name) {
		this.name = name
	},
	getUserName() {
		return this.name
	}
}

// 全局函数，用var或者直接声明，可以用window来调用

// 匿名函数
// 匿名函数不会提升（类似于变量提升）
test1() // 错误
let test1 = function() {
	console.log('test')
}
test1() // 正常
console.log(test1 instanceof Object) // true

// 立即执行函数
// 用括号括起来
```

#### 参数

```js
// a,b 是形参
// 123 是默认参数 默认参数放后面
function sum(a, b = 123) {
	return a + b
}
// 1,2 是实参
sum(1, 2) // 1+2=3
sum(1) // 1+123=124

function test(a) {
	return a <= 3
}

let arr = [1, 2, 3, 4, 5, 6, 7].filter(test)
console.log(arr)

function sum2(...args) {
	console.log(args) // [1,2,4]
	console.log([...arguments]) // [1,2,4]
	return args.reduce((a, b) => a + b)
}
sum2(1, 2, 4)
```

#### 箭头函数

```js
const test = () => console.log('test')
let arr = [1, 2, 3, 4, 5, 6].filter(a => a >= 3)
console.log(arr)

let sum = [1, 2, 3, 4].reduce((a, b) => a + b)
console.log(sum)
```

#### 递归函数

```js
function factorial(num) {
	// if (num === 1) {
	// 	return 1
	// }
	// return num * factorial(num - 1)
	return num === 1 ? 1 : num * factorial(num - 1)
}
factorial(5) // 120

function sum(...args) {
	return args.length === 0 ? 0 : args.pop() + sum(...args)
}
sum(1, 2, 3)
```

#### 回调函数

`在其他函数中调用的函数`

```js
document.getElementById('id').addEventListener('click', function() {
	console.log('回调函数')
})

let arr = [1, 2, 3, 4]
arr.map(function(v) {
	return v
})
```

#### 函数中的 this

```js
let obj = {
	name: 'sanm',
	getName() {
		return this.name
	},
	test: function() {
		return console.log('test')
	}
}
```

- 全局对象中 this 就是 window
- 在当前对象 this 就是当前对象
- 字面量，构造函数内部的 this 就是指当前对象，里面的函数指向的还是 window

```js
let obj2 = {
	list: ['baidu', 'google', 'github'],
	show: function() {
		// 如果在map中不用箭头函数而是用function回调函数，里面的this将指向window
		// 箭头函数会是this指向他的上一层级（父级作用域，上下文）
		return this.list.map(v => `${v}.com`)
	}
}
```

#### call、apply、bind

```js
function User(name) {
	this.name = name
}
let test = new User('张三')
console.log(test)
let test2 = { age: 27 }
User.call(test2, '大头')
console.log(test2)
// call 和 apply 的区别
// 传参不同
// call多个参数用逗号分隔，apply多个参数放数组内
// 第一个参数都是要改变this的对象，第二个是参数相关
// 都会立即执行一般函数
let arr = [1, 2, 3, 4, 5]
console.log(Math.max(...arr))
console.log(Math.max.apply(Math, arr))

// bind 不会立即执行，生成一个新的函数和call类似
// 有两次传参的机会
```
