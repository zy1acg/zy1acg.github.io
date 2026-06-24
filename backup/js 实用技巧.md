## 显性字符串转数字
```javascript
const str = '10';
const num = +str; //字符串转数字
```

## 显性转boolean
`const bool = !!'true';`

## 浮点数计算精度问题
- 如果对精度不敏感， 可以考虑 `toFixed` 方法进行小数截取
```js
console.log((0.1 + 0.2).toFixed(2)) //0.3

console.log(1.0 - 0.9) //0.09999999999999998
console.log((1.0 - 0.9).toFixed(2)) //0.10
```
- 将小数转为整数进行计算后，再转为小数也可以解决精度问题
```js
Number.prototype.add = function (num) {
	//取两个数值中小数位最大的
  let n1 = this.toString().split('.')[1].length
  let n2 = num.toString().split('.')[1].length

  //得到10的N次幂
  let m = Math.pow(10, Math.max(n1, n2))

  return (this * m + num * m) / m
}
console.log((0.1).add(0.2))
```
> [!important]
> 推荐做法
> 市面上已经存在很多针对数学计算的库 [mathjs](https://mathjs.org/examples/browser/basic_usage.html.html) 、[decimal.js](http://mikemcl.github.io/decimal.js) 等，我们就不需要自己构建了。下面来演示使用 [decimal.js](http://mikemcl.github.io/decimal.js) 进行浮点计算。
```js
<script src="https://cdn.bootcss.com/decimal.js/10.2.0/decimal.min.js"></script>

<script>
	console.log(Decimal.add(0.1, 0.2).valueOf())
</script>
```

## Math.random
- 取 minValue~maxValue 的随机数（不包括 maxValu）
  - 公式为:minValue+Math.floor(Math.random()*(maxValue -minValue))
- 取 minValue~maxValue 的随机数（包括 maxValu）
  - 公式为:minValue+Math.floor(Math.random()*(maxValue -minValue + 1))

## 展开语法
- 将类数组对象转为真正的数组
- 替代concat，合并数组
- 替代arguments，接受任意数量的函数参数，也可以用于接收部分参数
- 