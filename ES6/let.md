# let 和 const 命令
  
# let 命令
```js
var tmp = 123;

if (true) {
  // 存在暂时性死区
  tmp = 'abc'; // ReferenceError
  typeof tmp; // ReferenceError
  let tmp;
}
```
暂时性死区”也意味着typeof不再是一个百分之百安全的操作。

比较隐蔽“死区”
```js
function bar(x = y, y = 2) {
  return [x, y];
}

bar(); // 报错 y还没声明就赋值给了x

let x = x;
```
# 块级作用域
考虑到环境导致的行为差异太大，应该避免在块级作用域内声明函数。如果确实需要，也应该写成函数表达式，而不是函数声明语句。
# const 命令
const只能保证这个指针是固定的
如果真的想将对象冻结，应该使用Object.freeze方法。
# 顶层对象的属性
let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。
```js
let b = 1;
window.b // undefined
```
# global 对象
下面代码将顶层对象放入变量global。
```js
// CommonJS 的写法
var global = require('system.global')();

// ES6 模块的写法
import getGlobal from 'system.global';
const global = getGlobal();
```