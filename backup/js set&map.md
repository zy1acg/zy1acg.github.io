一句话概括：**`Set` 是“不重复的值集合”，`Map` 是“键可以是任意类型的键值对字典”。**

* * *

### 一、 相同点

1.  **都是 ES6 新增的集合类型**：专门用于存储和操作数据集合。
2.  **都是可迭代的（Iterable）**：都支持 `for...of` 循环、扩展运算符 `...` 以及 `Array.from()`。
3.  **保持插入顺序**：遍历时的顺序就是元素添加时的顺序。
4.  **都有 `size` 属性**：可以直接通过 `.size` 获取元素个数（不需要像数组用 `.length`，对象则需要 `Object.keys().length`）。
5.  **共有部分方法**：都有 `has()`、`delete()`、`clear()` 方法。
6.  **底层比较算法相同**：都使用 **Same-value-zero equality** 算法。它类似于严格相等 `===`，但有两个关键区别：
    +   `NaN` 等于 `NaN`（在 `===` 中 `NaN !== NaN`）。
    +   `+0` 等于 `-0`。

* * *

### 二、 核心区别

表格

| 维度  | `Set`(集合) | `Map`(字典/映射) |
| --- | --- | --- |
| **存储结构** | **单列值**（只有 value） | **键值对**（key - value） |
| **唯一性约束** | **值**必须唯一，重复添加会被忽略 | **键**必须唯一，重复设置会覆盖旧值 |
| **添加元素 API** | `.add(value)` | `.set(key, value)` |
| **获取元素 API** | 无直接获取方法（因为值就是键） | `.get(key)` |
| **键的类型限制** | 没有键的概念 | **任意类型**（对象、函数、NaN、基本类型均可） |
| **默认迭代器** | `values()` | `entries()` (返回 `[key, value]`) |
| **与 Object 对比** | 类似去重后的数组 | 类似 Object，但键不限于字符串/Symbol |

#### 代码直观对比：

javascript

编辑

```
// --- Set ---
const mySet = new Set();
mySet.add(1);
mySet.add("1");   // 严格区分类型，"1" 和 1 是不同的值
mySet.add(NaN);
mySet.add(NaN);   // NaN 被认为是相同的，不会重复添加
console.log(mySet.size); // 3

// --- Map ---
const myMap = new Map();
const objKey = { id: 1 };

myMap.set("name", "张三");     // 字符串作键
myMap.set(objKey, "对象键");   // 对象作键 (普通 Object 做不到)
myMap.set(NaN, "我是NaN");     // NaN 作键

console.log(myMap.get(objKey)); // "对象键"
console.log(myMap.size);        // 3
```

* * *

### 三、 使用注意事项（⚠️ 避坑指南）

#### 1\. 引用类型的“地址”比较陷阱（最常见错误）

`Set` 去重和 `Map` 判断键是否存在时，对于**对象/数组等引用类型**，比较的是**内存地址**，而不是内容。

javascript

编辑

```
const set = new Set();
set.add({ name: "张三" });
set.add({ name: "张三" }); 
console.log(set.size); // 2！因为这是两个不同的对象，内存地址不同

const map = new Map();
map.set({ id: 1 }, "A");
console.log(map.get({ id: 1 })); // undefined！因为 {id:1} 是一个新对象，地址不同
```

**解决思路**：如果需要根据对象内容去重或查找，应将其序列化为字符串（如 `JSON.stringify`）作为键，或提取唯一标识符（如 `id`）作为键。

#### 2\. Map 的键是“绑定”到对象引用的

如果使用对象作为 `Map` 的键，只要这个 `Map` 存在，该对象就不会被垃圾回收（即使外部已经没有变量引用它了），这**极易引发内存泄漏**。

javascript

编辑

```
let map = new Map();
let domNode = document.getElementById('app');
map.set(domNode, '一些数据');

// 假设后来页面上 #app 节点被删除了
// domNode = null; 
// 只要 map 还在，这个 domNode 的内存就永远不会被释放！
```

**解决思路**：如果键是 DOM 节点或对象，且希望外部销毁时自动释放内存，请使用 **`WeakMap`**。

#### 3\. JSON 序列化问题

`Set` 和 `Map` **不能直接通过 `JSON.stringify()` 正确转换**。

javascript

编辑

```
const set = new Set([1, 2, 3]);
const map = new Map([['a', 1]]);

JSON.stringify(set); // "{}" (空对象)
JSON.stringify(map); // "{}" (空对象)
```

**解决思路**：在序列化前，先转换为数组。

javascript

编辑

```
JSON.stringify([...set]);            // "[1,2,3]"
JSON.stringify(Array.from(map));     // '[["a",1]]'
// 或者使用 replacer 函数自定义序列化逻辑
```

#### 4\. 不要用 `forEach` 中的 `break`

`Set` 和 `Map` 的 `.forEach()` 方法**无法使用 `break` 或 `return` 提前终止循环**（和数组的 `forEach` 一样）。如果需要提前终止遍历，请使用 `for...of`。

javascript

编辑

```
for (const [key, value] of myMap) {
  if (key === 'target') break; // 可以正常 break
}
```

#### 5\. 性能考量

+   **频繁增删**：在需要频繁添加、删除元素的场景下，`Set` 和 `Map` 的性能通常优于 `Array` 和 `Object`。
+   **内存占用**：`Set` 和 `Map` 的底层实现比简单的数组/对象复杂，因此在存储少量数据时，内存占用可能会略高。

* * *

### 四、 典型应用场景总结

表格

| 场景  | 推荐数据结构 | 示例  |
| --- | --- | --- |
| **数组去重** | `Set` | `[...new Set(arr)]` |
| **交集/并集/差集** | `Set` | 利用 `filter` 和 `has` 实现集合运算 |
| **保存唯一回调函数列表** | `Set` | 事件总线（EventBus）中防止重复注册同一个回调 |
| **用对象/DOM节点做键** | `Map` | 给 DOM 节点绑定私有数据，不污染 DOM 属性 |
| **缓存计算结果** | `Map` | 以参数为 key，结果为 value，实现 Memoize（记忆化） |
| **保持键的插入顺序** | `Map` | 普通 Object 在早期 JS 中不保证顺序，Map 严格保证 |

* * *

### 补充：什么时候用 `WeakSet` / `WeakMap`？

当你需要以**对象**作为 `Set` 的值或 `Map` 的键，且**不希望阻止垃圾回收**时，使用 `Weak` 系列：

+   **`WeakSet`**：只能存对象。适合记录“某个对象是否被处理过”（如标记已遍历的节点），对象销毁时自动从 WeakSet 消失。
+   **`WeakMap`**：键只能是对象。适合给对象附加“私有数据”或缓存。当对象被销毁时，对应的键值对自动消失，不会内存泄漏。

javascript

编辑

```
// WeakMap 经典应用：给 DOM 节点存数据
const wm = new WeakMap();
const btn = document.querySelector('#btn');
wm.set(btn, { clickCount: 0 });

btn.addEventListener('click', () => {
  let data = wm.get(btn);
  data.clickCount++;
});
// 当 btn 从页面移除且无其他引用时，wm 里的数据会被自动垃圾回收。
```
在 JavaScript 中，`Set` 和 `Map` 是 ES6 引入的两种全新数据结构，用于弥补传统 `Array` 和 `Object` 在特定场景下的不足。