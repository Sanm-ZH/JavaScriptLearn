### 正则表达式

#### 字面量创建

```js
let str = 'abc'
let t = 'c'
// true
console.log(/c/.test(str))
// 使用变量
console.log(eval(`/${t}/`).test(str)))
```

#### 对象创建

```js
let str = 'abc'
let t = 'c'
let reg = new RegExp(t, 'g')
// false
console.log(reg.test(str))
```

> **实例**

```html
<div>dididi1234567</div>
```

```js
// 输入字符，使输入字符高亮(替换)

// prompt浏览器输入弹框
let imp = prompt('输入要检测的内容,支持正则表达式')
let reg = new RegExp(imp, 'g')
let doc = document.querySelector('div')
doc.innerHTML = doc.innerHTML.replace(reg, search => {
	return `<span style="color: red">${search}</span>`
})
```

#### 选择符与(原子表|原子组)中的选择符

```js
// 匹配号码
let tel = '010-8888888'
console.log(/(010|020)\-\d{7, 8}/.test(tel))
```

```js
// 12|34
let reg1 = /(12|34)/
// 1|2|3|4
let reg2 = /[1234]/
let str = '1234'
console.log(str.match(reg1))
```

#### 转义运用

```js
let price = 414.603
//.除换行外任意字符 \.普通点
// d \d 数字
console.log(/\d+\.\d/.test(price))
console.log('d' == 'd')
let reg = new RegExp('\\d+\\.\\d+')
console.log(reg.test(price))

// 网址
let url = 'https://www.github.com'
console.log(/https?:\/\/\w+\.\w+\.\w/.test(url))
```

#### 字符的边界

```js
let str = 'abc123defg'
// ^开始边界 $结束边界
console.log(/^\d$/.test(str))
```

> 实例

```html
<input type="text" name="user"></input>
<span></span>
```

```js
document.querySelector('[name="user"]').addEventListener('keyup', function() {
	let flag = this.value.match(/^[a-z]{3, 6}$/)
	document.querySelector('span').innerHTML = flag ? '正确' : '错误'
})
```

#### 元字符

```js
let str = 'sanmzh 2019'
// \d匹配数字 g全部
console.log(str.match(/\d+/g/))

let call = '张三: +86-13912341234,李四: +86-18912341234'
console.log(call.match(/\+\d{2}-\d{11}/g))

// \D匹配非数字
console.log(str.match(/\D+/))
// [^xxx] 除了xxx符合
console.log(call.match(/[^-\d:,]/g))

// \s 空白 \S除了空白
console.log(/\s/.test('\nzs'))
console.log(/\S/.test(' \nzs'))

// \w 字母数字下划线
let str2 = '123agcd_++++'
console.log(str2.match(/\w+/))
let email = '12345@qq.com'
console.log(email.match(/^\w+@\w+\.\w+$/))
console.log('123@'.match(/\W/)) // @

// 表单用户名
/^[a-z]\w{6, 9}$/ //字母开始，字母数字下划线结尾，6~9位

// .除换行的所有字符
let url = 'http://www.github.com'
console.log(url.match(/https?:\/\/\w+\.\w+\.\w+/))

// /s 单行匹配,s模式
let str3 = `
123
agc
1234afdsfa
`
console.log(str3.match(/.+/)) // 123
console.log(str3.match(/.+/s)[0])
```

> 实例

```js
let tem = `
<span>
	github 123
	sanmzh
</span>
`
// [\s\S] [\d\D] [a-z]
console.log(tem.match(/<span>[\d\D]+<\/span>/))
```

#### 模式修正符

```js
let str = '123AbcAbc'
// i 忽略大小写 g 全局
console.log(str.match(/a/gi))

console.log(str.replace(/a/gi, '++'))

// m 多行匹配
let str2 = `
#1 git,100 #
#2 svn,60 #
#3 123,55 # 1231
#3 box,55 #
`
// * 0个或多个 +一个或多个
console.log(str2.match(/^\s*#\d+\s+.+\s+#$/gm))
let obj = str2.match(/^\s*#\d+\s+.+\s+#$/gm).map(v => {
	v = v.replace(/\s*#\d+\s*/, '').replace(/\s+#/, '')
	let [name, sum] = v.split(',')
	return { name, sum }
})
console.log(JSON.stringify(obj, null, 2))
// 宽字符也可以用 u 模式
let str3 = 'github 三'
console.log(str3.match(/\p{L}/gu))
console.log(str3.match(/\p{P}/gu))
console.log(str3.match(/\p{sc=Han}/gu))
```

**lastIndex 属性的作用**

```js
// g 全局模式下标识才会走
let str4 = 'github123'
let reg = /\w/g
console.log(reg.lastIndex)
console.log(reg.exec(str4))
console.log(reg.lastIndex)
console.log(reg.exec(str4))
while ((res = reg.exec(str4))) {
	console.log(res)
}

// y模式 连续满足
let str5 = `发生的发生的1234,1234,124,1234,132123阿凡达撒`
reg = /(\d+),?/y
reg.lastIndex = 6
let sums = []
while ((res = reg.exec(str5))) {
	sums.push(res[1])
}
console.log(sums)
```

#### 原子表

```js
let str = 'github'
console.log(str.match(/[gtub]+/g))
let str2 = '1993-08-15'
// 后面的\1取前面第一个原子组，既保证-/要统一
let reg = /^\d{4}([-\/])\d{1,2}\1\d{1,2}$/
console.log(str2.match(reg))

// 区间匹配
let str3 = '12345abc'
// [0-9] [a-z] 不能降序
console.log(str3.match(/[0-9]+/g))
console.log(str3.match(/[a-z]+/g))
console.log(str3.match(/^[a-z]\w{3, 6}$/i))

// 排除匹配
// [^\d]
console.log(str3.match(/[^\d]+/g))
```

`ps: 原子表内大多数字符是不解释的，只是当做普通的字符`

> 实例

```html
<p>sanm</p>
<h1>zh</h1>
<h2>github</h2>
```

```js
let body = document.body
let reg = /<(h[1-6])[\s\S]*<\/\1>/gi
body.innerHTML = body.innerHTML.replace(reg, '')
```

#### 原子组

```js
// 用括号括起来
// 编号 \1 \2 从左到右取组里面的内容
let reg = /<(h[1-6])[\s\S]*<\/\1>/gi

// 校验邮箱
let mail = document
	.querySelector('[name="mail"]')
	.addEventListener('keyup', function() {
		let reg = /^[\w-]+@([\w-]+\.)+(com|org|cc|cn|net)$/i
		console.log(reg.test(this.value))
	})

let str = `
	<h1>sanmzh</h1>
	<span>github</span>
	<h2>dididi</h2>
`
let reg2 = /<(h[1-6])>([\s\S]+)<\/\1>/gi
// $2 取第二个组里面的内容
console.log(str.replace(reg2, `<p>$2</p>`))
// 数左括号(确定下标是哪个 从1开始  p0是全部内容
str.replace(reg2, (v, p1, p2) => `<p>${p2}</p>`)

// 嵌套分组和不记录分组
let url = `
https://www.github.com
http://github.com
`
// ?: 不记录到组编号中
let reg3 = /https?:\/\/((?:\w+\.)?\w+\.(?:com|cn|org))/gi
// console.dir(url.match(reg3))
let urls = []
// exec遍历出匹配结果，取p1
while ((res = reg3.exec(url))) {
	urls.push(res[1])
}
console.log(urls)
```

> 原子组别名

```js
// ?<name> 给组命名
let html = `
	<a href="https://github.com">github</a>
	<a href="http://sanm-zh.github.io">blog</a>
`
let reg = /<a.*?href=(['"])(?<link>.*?)\1>(?<title>.*?)<\/a>/gi
let links = []
for (const iter of html.matchAll(reg)) {
	links.push(iter['groups'])
}
console.log(links)
```

---

> 实例 禁止贪婪

```html
<main>
	<span>123</span>
	<span>456</span>
	<span>789</span>
</main>
```

```js
const main = document.querySelector('main')
const reg = /<span>([\s\S]+?)<\/span>/gi
// ?
main.innerHTML = main.innerHTML.replace(reg, (v, p1) => {
	return `<h4 style="color: red">sanm-${p1}</h4>`
})
```

> 实例 matchALL 全局匹配

```html
<body>
	<h1>123</h1>
	<h2>456</h2>
	<h1>789</h1>
</body>
```

```js
const body = document.body
const reg = /<(h[1-6])>([\s\S]+?)<\/\1>/gi
let contents = []
// matchAll 高版本浏览器
const iters = body.innerHTML.matchAll(reg)
for (const iter of iters) {
	contents.push(iter[2])
}
console.table(contents)

// 适配老浏览器
String.prototype.matchALL = function(reg) {
	let res = this.match(reg)
	if (res) {
		let str = this.replace(res[0], '^'.repeat(res[0].length))
		let match = str.matchAll(reg) || []
		return [res, ...match]
	}
}
```

> 实例 exec 匹配全局

```js
let str = 'www.github.com'
let reg = /\./gi
let result = []
while ((res = reg.exec(str))) {
	result.push(res)
}
```

> 实例 字符串的一些支持正则的方法

```js
let str = 'github'
// serach可用用正则或字符 返回下标
console.log(str.search(/h/))
// match 不加g只返回一个
console.log(str.match(/h/))
// matchAll会返回一个迭代器，结果遍历

// split
let t = '2019-12-26'
console.log(t.split(/[-\/]/))
```

> 正则的一些方法

- test 返回一个布尔类型
- exec 返回一个迭代器
- 单次匹配和 match 类似，全局匹配会有细节

---

#### \$ &的使用

```js
// 正则内是开始
// $1 $2 组编号
// $` 匹配前面的内容  $' 匹配后面的内容
let str = 'left张三right'
console.log('左', str.replace(/张三/, '$`'))
console.log('右', str.replace(/张三/, "$'"))

let str = '这是我的GitHub'
let content = str.replace(/github/i, `<a href="sanm-zh.github.io">$&</a>`)
console.log(content)
```

#### 断言匹配

```js
let str = 'github, 这是我的github博客'
// ?= 后面是
let reg = /github(?=博客)/gi
console.log(str.replace(reg, `<a href="https://sanm-zh.github.io">$&</a>`))

// ?<= 前面是
let str2 = 'sanm123'
let reg2 = /(?<=sanm)\d+/gi
console.log(str2.match(reg2))

// 给电话号码中间四位加上*号
let phones = `
	张三：13912348888
	李四：18912348888
`
let reg3 = /(?<=\d{3})\d+(?=\d{4})/gi
phones = phones.replace(reg3, v => {
	return '*'.repeat(4)
})
console.log(phones)

// ?! 后面不是
let str4 = 'sanm2017github'
let reg4 = /[a-z]+(?!\d)$/i
console.log(str4.match(reg4))
// ?<! 前面不是
let reg5 = /(?<!\d+)[a-z]+/i
console.log(str4.match(reg5))
```
