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
