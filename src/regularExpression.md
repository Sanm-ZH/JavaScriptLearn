### 正则表达式

#### 字面量创建

```js
let str = 'abc'
let t = 'c'
// true
console.log(/c/.test(str))
// 使用变量
console.log(eval(`/${t}/`.test(str)))
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

#### 选择符&原子表|原子组中的选择符

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
