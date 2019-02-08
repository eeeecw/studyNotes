# 正则的扩展

# RegExp 构造函数
```js
new RegExp(/abc/ig, 'i').flags
// "i"
```

# 字符串的正则方法
字符串对象共有 4 个方法，可以使用正则表达式：match()、replace()、search()和split()。

# u 修饰符
## （1）点字符
对于码点大于0xFFFF的 Unicode 字符，点字符不能识别，必须加上u修饰符。
## （2）Unicode 字符表示法
ES6 新增了使用大括号表示 Unicode 字符，这种表示法在正则表达式中必须加上u修饰符，才能识别当中的大括号，否则会被解读为量词。
## （3）量词
使用u修饰符后，所有量词都会正确识别码点大于0xFFFF的 Unicode 字符。
## （4）预定义模式
```js
/^\S$/.test('𠮷') // false
/^\S$/u.test('𠮷') // true
```
## （5）i 修饰符
```js
/[a-z]/i.test('\u212A') // false
/[a-z]/iu.test('\u212A') // true
```
# RegExp.prototype.unicode 属性
正则实例对象新增unicode属性，表示是否设置了u修饰符。

# y 修饰符
y修饰符的设计本意，就是让头部匹配的标志^在全局匹配中都有效。
```js
const REGEX = /a/gy;
'aaxa'.replace(REGEX, '-') // '--xa'
```
y修饰符确保了匹配之间不会有漏掉的字符。

# RegExp.prototype.sticky 属性
是否设置了y修饰符。

# RegExp.prototype.flags 属性
返回正则表达式的所有修饰符。

# s 修饰符：dotAll 模式
通过 `s` 修饰符 点 可以匹配所有<br>
新增 `dotAll` 属性
```js
const re = /foo.bar/s;

re.test('foo\nbar') // true
re.dotAll // true
re.flags // 's'
```
# 后行断言
🍎 没看

# Unicode 属性类
🍎 没看

# 具名组匹配
```js
const RE_DATE = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;

const matchObj = RE_DATE.exec('1999-12-31');
const year = matchObj.groups.year; // 1999
const month = matchObj.groups.month; // 12
const day = matchObj.groups.day; // 31
```

有了具名组匹配以后，可以使用解构赋值直接从匹配结果上为变量赋值。
```js
let {groups: {one, two}} = /^(?<one>.*):(?<two>.*)$/u.exec('foo:bar');
one  // foo
two  // bar
```
字符串替换时，使用$<组名>引用具名组。
```js
let re = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/u;

'2015-01-02'.replace(re, '$<day>/$<month>/$<year>')
// '02/01/2015'
```

# String.prototype.matchAll

返回一个遍历器，而不是数组