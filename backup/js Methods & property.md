## js Methods & property
### String
- .length			字符串长度
- .toString()		将对象转换为字符串
- .toUpperCase()	将字符串转换为大写
- .toLowCase()		 将字符串转换为小写
- .trim()			删除字符串两端的空白字符
- .trimLeft()		删除字符串左侧的空白字符
- .trimRight()		删除字符串右侧的空白字符
- .charAt()		返回指定索引位置的字符
- [index]			返回指定索引位置的字符
- .slice()			提取字符串的一部分并返回新字符串
- .substring()		提取两个指定索引位置之间的字符
- .indexOf()		返回指定值在字符串中首次出现的位置
- .lastIndexOf()	返回指定值在字符串中最后出现的位置
- .search()		检索字符串中指定的子字符串或正则表达式
- .includes()		判断一个字符串是否包含在另一个字符串中，返回布尔值
- .startsWith()		判断一个字符串是否以指定的子字符串开头
- .endsWith()		判断一个字符串是否以指定的子字符串结尾
- .replace()		在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串
- .repeat()		将字符串重复指定次数并返回
- .split()			使用指定的分隔符将一个字符串分割成一个字符串数组

### Number
- .isInteger()		判断一个值是否为整数
- .toFixed()		将数字格式化为指定小数位数的字符串
- .isNaN()			判断一个值是否为NaN
- parseInt()		提取字符串开始去除空白后的数字转为整数，解析一个字符串并返回指定基数的整数
- parseFloat()		转换字符串为浮点数，忽略字符串前面空白字符，解析一个字符串并返回一个浮点数

### Math
- Math.min()		返回零个或多个数中的最小值。
- Math.max()		返回零个或多个数中的最大值。
- Math.ceil()		返回大于或等于一个给定数字的最小整数（向上取整）。
- Math.floor()		返回小于或等于一个给定数字的最大整数（向下取整）。
- Math.round()	返回一个数字四舍五入后最接近的整数。
- Math.random()	返回一个 0 到 1 之间的伪随机数。
- Math.pow()		返回基数（base）的指数（exponent）次幂。 

### Array
- .every()			是否能通过回调函数的测试
- .some()			至少有一个通过测试函数
- .reduce()		循环函数传递当前和上一个值，对数组中的每个元素执行一个由您提供的 reducer 函数，将其结果汇总为单个返回值
- .map()			创建一个新数组，其结果是该数组中的每个元素都调用一次提供的函数后的返回值
- .join(): 将数组	（或类数组对象）的所有元素连接成一个字符串

### Object
- Object.freeze	冻结修改
- Object.is()		是否完全相等

### Date
- Date.now(): 		返回自 1970 年 1 月 1 日 00:00:00 UTC 到当前时间的毫秒数
- getTime():  		返回自 1970 年 1 月 1 日 00:00:00 UTC 到该日期对象的毫秒数
- getFullYear():  	根据本地时间返回指定日期的年份
- getMonth():  	根据本地时间返回指定日期的月份（0-11）
- getDate():  		根据本地时间返回指定日期的月份中的某一天（1-31）
- getHours():  		根据本地时间返回指定日期的小时数（0-23）
- getMinutes():  	根据本地时间返回指定日期的分钟数（0-59）
- getSeconds():  	根据本地时间返回指定日期的秒数（0-59）
- valueOf():  		返回日期对象的原始值（毫秒数）

### Other
- console.log(): 向 Web 控制台输出一条信息。
- console.dir(): 以交互方式在控制台中显示指定 JavaScript 对象的属性列表。
- console.time(): 启动一个计时器，用于计算一个操作的持续时间。
- console.timeEnd(): 停止一个由 console.time() 启动的计时器，并在控制台输出经过的时间。
- prompt(): 显示一个对话框，提示用户输入文本。
- alert(): 显示一个带有一段消息和一个确认按钮的警告框。
- document.querySelector(): 返回文档中与指定选择器或选择器组匹配的第一个元素。
- document.write(): 向文档写入 HTML 表达式或 JavaScript 代码。
- apply(): 调用一个函数，并指定其 this 值和以数组形式提供的参数。

### 操作符
- typeof xxx
- xxx instanceof xxx