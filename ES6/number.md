# 数值的扩展

# 二进制和八进制表示法
二进制前缀 `0b` 或 `0B`<br>
八进制前缀 `0o` 或 `0O`

# Number.isFinite(), Number.isNaN()
它们与传统的全局方法 isFinite() 和 isNaN() 的区别在于:传统方法先调用Number()将非数值的值转为数值，再进行判断。

# Number.parseInt(), Number.parseFloat()
全局方法移植过来，特性不变。

# Number.isInteger()
判断一个数值是否为整数
```js
Number.isInteger(3.0000000000000002) // true
// 小数的精度达到了小数点后16个十进制位，转成二进制位超过了53个二进制位，导致最后的那个2被丢弃了。
```
❄️ 如果一个数值的绝对值小于Number.MIN_VALUE（5E-324）,会被自动转为 0。这时，`Number.isInteger` 也会误判。

# Number.EPSILON
Number.EPSILON的实质是一个可以接受的最小误差范围。
```js
function withinErrorMargin (left, right) {
  return Math.abs(left - right) < Number.EPSILON * Math.pow(2, 2);
}

0.1 + 0.2 === 0.3 // false
withinErrorMargin(0.1 + 0.2, 0.3) // true

1.1 + 1.3 === 2.4 // false
withinErrorMargin(1.1 + 1.3, 2.4) // true
```
# 安全整数和 Number.isSafeInteger()
JavaScript 能够准确表示的整数范围在-2^53到2^53之间
```js
Number.MAX_SAFE_INTEGER === Math.pow(2, 53) - 1  // true
Number.MAX_SAFE_INTEGER === 9007199254740991  // true

Number.MIN_SAFE_INTEGER === -Number.MAX_SAFE_INTEGER  // true
Number.MIN_SAFE_INTEGER === -9007199254740991  // true
```
# Math 对象的扩展
## Math.trunc
Math.trunc方法用于去除一个数的小数部分，返回整数部分。对于非数值，Math.trunc内部使用Number方法将其先转为数值。对于空值和无法截取整数的值，返回NaN。

## Math.sign
Math.sign方法用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值。

## Math.cbrt
Math.cbrt方法用于计算一个数的立方根
🍎 还有好多，没写进来

# 指数运算符
```js
2 ** 3 ** 2
// 相当于 2 ** (3 ** 2)

b **= 3;
// 等同于 b = b * b * b;
```