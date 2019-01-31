# 变量的解构赋值

# 数组的解构赋值

## 基础用法
构不成功，变量的值就等于undefined。
```js
let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []
```

不完全解构
```js
let [a, [b], d] = [1, [2, 3], 4];
a // 1
b // 2
d // 4
```
事实上，只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。
```js
function* fibs() {
  let a = 0;
  let b = 1;
  while (true) {
    yield a;
    [a, b] = [b, a + b];
  }
}

let [first, second, third, fourth, fifth, sixth] = fibs();
sixth // 5
```

## 默认值
```js
let [x = 1] = [null];
x // null
```

# 对象的解构赋值
下面代码有三次解构赋值，分别是对loc、start、line三个属性的解构赋值。注意，最后一次对line属性的解构赋值之中，只有line是变量，loc和start都是模式，不是变量。
```js
const node = {
  loc: {
    start: {
      line: 1,
      column: 5
    }
  }
};

let { loc, loc: { start }, loc: { start: { line }} } = node;
line // 1
loc  // Object {start: Object}
start // Object {line: 1, column: 5}
```

下面将一个已经声明的变量用于解构赋值,JavaScript 引擎会将{x}理解成一个代码块，从而发生语法错误。
```js
// 错误的写法
let x;
{x} = {x: 1};

// 正确的写法
let x;
({x} = {x: 1});
```
# 字符串的解构赋值

类似数组的对象都有一个length属性，因此还可以对这个属性解构赋值。
```js
let {length : len} = 'hello';
len // 5
```
# 数值和布尔值的解构赋值
解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。由于 `undefined` 和 `null` 无法转为对象，所以对它们进行解构赋值，都会报错。
```js
let { prop: x } = undefined; // TypeError
let { prop: y } = null; // TypeError
let {toString: s} = true;
s === Boolean.prototype.toString // true
```
# 函数参数的解构赋值
函数参数的解构也可以使用默认值。undefined就会触发函数参数的默认值。
```js
[1, undefined, 3].map((x = 'yes') => x);
```
# 圆括号问题
- 不可以使用
1.变量声明语句
2.函数参数
3.赋值语句的模式
- 可以使用
1.赋值语句的非模式部分

# 用途

## (1).交换变量的值

## (2).从函数返回多个值

## (3).函数参数的定义

## (4).提取 JSON 数据

## (5).函数参数的默认值

## (6).遍历 Map 结构
```js
const map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
```
## (7).输入模块的指定方法
```js
const { SourceMapConsumer, SourceNode } = require("source-map");
```