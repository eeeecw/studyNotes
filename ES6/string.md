# 字符串的扩展

# 字符的 Unicode 表示法
JavaScript 共有 6 种方法可以表示一个字符
```js
'\z' === 'z'  // true
'\172' === 'z' // true
'\x7A' === 'z' // true
'\u007A' === 'z' // true
'\u{7A}' === 'z' // true
```

# codePointAt()
JavaScript 内部，字符以 UTF-16 的格式储存，每个字符固定为2个字节。对于那些需要4个字节储存的字符（Unicode 码点大于0xFFFF的字符），JavaScript 会认为它们是两个字符。
```js
let s = '𠮷a';
for (let ch of s) {
  console.log(ch.codePointAt(0).toString(16));
}
```

# String.fromCodePoint()
弥补了String.fromCharCode方法的不足。

# 字符串的遍历器接口
字符串可以被for...of循环遍历,可以识别大于0xFFFF的码点。

# normalize()
我理解就是为了欧洲国家使用，原字符与重音符号的合成一个字符。
```js
'\u01D1'==='\u004F\u030C' //false
'\u01D1'.normalize() === '\u004F\u030C'.normalize() // true
```
# includes(), startsWith(), endsWith()
使用第二个参数n时，endsWith的行为与其他两个方法有所不同。它针对前n个字符，而其他两个方法针对从第n个位置直到字符串结束。
```js
s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
````
# repeat()
repeat方法返回一个新字符串，表示将原字符串重复n次。
参数会向下取整
0 到-1 之间的小数，则等同于 0
参数NaN等同于 0。

# padStart()，padEnd()
padStart()用于头部补全，padEnd()用于尾部补全。
一共接受两个参数，第一个参数是字符串补全生效的最大长度，第二个参数是用来补全的字符串。
```js
// 用途1:为数值补全指定位数。
'1'.padStart(10, '0') // "0000000001"
'12'.padStart(10, '0') // "0000000012"
'123456'.padStart(10, '0') // "0000123456"

// 用途2:提示字符串格式
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```

# matchAll()
看《正则扩展》

# 模板字符串
🍎引用模板字符串本身,没看懂
```js
// 写法一
let str = 'return ' + '`Hello ${name}!`';
let func = new Function('name', str);
func('Jack') // "Hello Jack!"

// 写法二
let str = '(name) => `Hello ${name}!`';
let func = eval.call(null, str);
func('Jack') // "Hello Jack!"
```
# 实例：模板编译
🍎后面这些都没看

# 标签模板

# String.raw()

# 模板字符串的限制
