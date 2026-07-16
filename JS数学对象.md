# JavaScript Math 数学对象知识点总结
## 一、Math 对象概述
Math 是 JavaScript 内置的数学工具对象，所有属性和方法都是静态的，**无需通过 `new` 创建实例**，直接通过 `Math.属性名` / `Math.方法名()` 即可调用。

---

## 二、核心方法详解
### 1. Math.abs() 计算绝对值
- **核心定义**：返回一个数字的绝对值（非负值）。正数返回本身，负数返回对应的正数，0 返回 0。
- **语法**：`Math.abs(数字)`
- **基础示例**：
```javascript
// 负数取绝对值
var num = -8;
console.log(Math.abs(num)); // 输出：8

// 正数取绝对值
var num2 = 8;
console.log(Math.abs(num2)); // 输出：8

// 0与小数的绝对值
console.log(Math.abs(0));      // 输出：0
console.log(Math.abs(-3.14));  // 输出：3.14
```
- **注意事项**：如果传入非数字类型，会先尝试隐式转换为数字；转换失败会返回 `NaN`。

---

### 2. Math.ceil() 向上取整
- **核心定义**：返回**大于或等于**该数字的最小整数。简单理解为：只要数字有小数部分，就向数值更大的方向进 1。
- **语法**：`Math.ceil(数字)`
- **基础示例**：
```javascript
// 正数向上取整
var num3 = 8.11;
console.log(Math.ceil(num3));   // 输出：9
console.log(Math.ceil(8.99));   // 输出：9

// 整数直接返回本身
console.log(Math.ceil(8));      // 输出：8

// 负数向上取整（往数值更大的方向，即靠近0）
var num4 = -8.11;
console.log(Math.ceil(num4));   // 输出：-8
console.log(Math.ceil(-8.99));  // 输出：-8
```
- **易错点**：负数向上取整不是“绝对值变大”，而是数值变大（更靠近 0），不要和正数的“进 1”直觉混淆。

---

### 3. Math.floor() 向下取整
- **核心定义**：返回**小于或等于**该数字的最大整数。简单理解为：直接舍弃小数部分，向数值更小的方向取整。
- **语法**：`Math.floor(数字)`
- **基础示例**：
```javascript
// 正数向下取整（等价于砍去小数部分）
var num5 = 8.11;
console.log(Math.floor(num5));  // 输出：8
console.log(Math.floor(8.99));  // 输出：8

// 整数直接返回本身
console.log(Math.floor(8));     // 输出：8

// 负数向下取整（往数值更小的方向，即远离0）
var num6 = -8.11;
console.log(Math.floor(num6));  // 输出：-9
console.log(Math.floor(-8.99)); // 输出：-9
```
- **易错点**：负数向下取整不是“去掉小数”。去掉 `-8.11` 的小数会得到 `-8`，但 floor 会得到更小的 `-9`。

---

### 4. Math.round() 四舍五入取整
- **核心定义**：对数字执行标准四舍五入，返回最接近的整数；当小数部分恰好为 0.5 时，**向数值更大的整数（正无穷方向）取整**。
- **语法**：`Math.round(数字)`
- **基础示例**：
```javascript
// 正数四舍五入
var num7 = 8.56;
console.log(Math.round(num7));  // 输出：9
console.log(Math.round(8.4));   // 输出：8
console.log(Math.round(8.5));   // 输出：9（小数0.5，向大取整）

// 负数四舍五入
var num8 = -8.50;
console.log(Math.round(num8));  // 输出：-8（0.5时往数值更大的方向，靠近0）
console.log(Math.round(-8.6));  // 输出：-9
console.log(Math.round(-8.4));  // 输出：-8
```
- **易错点**：`Math.round(-8.5)` 结果是 `-8`，不是 `-9`，这是和日常直觉最容易冲突的地方。
- **扩展技巧**：保留 n 位小数 → 先乘 10ⁿ → 取整 → 再除以 10ⁿ。
  示例（保留2位小数）：`Math.round(num * 100) / 100`

---

### 5. Math.random() 生成随机数
- **核心定义**：生成一个 `[0, 1)` 之间的伪随机浮点数，**包含 0，不包含 1**。
  
  > ❌ 原笔记注释“不包括0”表述错误，正确范围是「包含0、不包含1」。
- **语法**：`Math.random()` 无参数
- **基础示例**：
```javascript
// 生成0~1的随机小数，每次运行结果不同
console.log(Math.random()); // 例如输出：0.123456789
```

#### 核心扩展公式（必背）
纯 0~1 的随机数很少直接使用，通常配合取整扩展为指定范围的随机数。
1. **生成 0 ~ n-1 的随机整数**（对应数组/字符串索引场景）
   公式：`Math.floor(Math.random() * n)`
   ```javascript
   // 生成0~9的随机整数（共10个可能值）
   console.log(Math.floor(Math.random() * 10));
   ```

2. **生成 min ~ max 的随机整数（首尾都包含）**
   公式：`Math.floor(Math.random() * (max - min + 1)) + min`
   ```javascript
   // 生成 1~100 之间的随机整数
   var min = 1;
   var max = 100;
   var result = Math.floor(Math.random() * (max - min + 1)) + min;
   console.log(result);
   ```

#### 实用场景示例
1. 从字符串中随机抽取一个字符
```javascript
var str = "dawdadnbibbnsadsjd";
// 随机生成合法的字符串索引
var randomIndex = Math.floor(Math.random() * str.length);
console.log(str.charAt(randomIndex));
```

2. 从数组中随机抽取一个元素（随机点名、抽奖）
```javascript
var str = "小红,小猪,小冬,小康,小夏";
var nameArr = str.split(","); // 分割为数组
// 随机生成数组下标
var randomIndex = Math.floor(Math.random() * nameArr.length);
console.log(nameArr[randomIndex]);
```

- **注意事项**：
  - 不接收参数，写 `Math.random(100)` 属于无效写法
  - 生成随机整数优先配合 `Math.floor`，用 `Math.round` 会导致首尾数字出现概率减半，分布不均
  - 属于伪随机数，满足普通开发、小游戏场景，不适合加密安全场景

---

### 6. Math.max() 求最大值
- **核心定义**：接收多个数字参数，返回其中的最大值。
- **语法**：`Math.max(数字1, 数字2, 数字3...)`
- **基础示例**：
```javascript
var maxNum = Math.max(1, 5, 3, 9, 2);
console.log(maxNum); // 输出：9

console.log(Math.max(-1, -5, -3)); // 输出：-1
```

- **数组求最大值写法**：配合展开运算符 `...` 拆开数组
```javascript
var arr = [12, 5, 28, 9, 15];
var max = Math.max(...arr);
console.log(max); // 输出：28
```

---

### 7. Math.min() 求最小值
- **核心定义**：接收多个数字参数，返回其中的最小值。
- **语法**：`Math.min(数字1, 数字2, 数字3...)`
- **基础示例**：
```javascript
var minNum = Math.min(1, 5, 3, 9, 2);
console.log(minNum); // 输出：1

console.log(Math.min(-1, -5, -3)); // 输出：-5
```

- **数组求最小值写法**：配合展开运算符 `...`
```javascript
var arr = [12, 5, 28, 9, 15];
var min = Math.min(...arr);
console.log(min); // 输出：5
```

---

### 8. Math.pow() 幂运算（求次方）
- **核心定义**：返回底数的指数次幂，即「底数^指数」的计算结果。
- **语法**：`Math.pow(底数（必写）, 指数（必写）)`
- **基础示例**：
```javascript
var base = 2;
var exponent = 3;
var power = Math.pow(base, exponent);
console.log(power); // 输出：8 （2的3次方 = 2*2*2）

console.log(Math.pow(3, 2));    // 输出：9（3的平方）
console.log(Math.pow(5, 0));    // 输出：1（任何非0数的0次幂都是1）
console.log(Math.pow(2, -2));   // 输出：0.25（负指数 = 倒数的正次幂）
```

---

## 三、易混淆取整方法对比
| 方法 | 8.1 | 8.9 | -8.1 | -8.9 | 核心规则 |
|------|-----|-----|------|------|----------|
| `Math.ceil()` | 9 | 9 | -8 | -8 | 往数值更大的方向取整 |
| `Math.floor()` | 8 | 8 | -9 | -9 | 往数值更小的方向取整 |
| `Math.round()` | 8 | 9 | -8 | -9 | 四舍五入，0.5 往大取 |

---

## 四、常见易错点汇总
1. Math 不需要 `new` 创建实例，直接调用静态方法和属性即可。
2. `Math.random()` 取值范围是 `[0, 1)`，包含 0、不包含 1。
3. 负数的取整方向容易搞反，记住核心原则：**向上=数值变大，向下=数值变小**。
4. `Math.max()` / `Math.min()` 不能直接传入数组，需要用展开运算符 `...` 把数组拆成独立参数。
5. 所有方法大小写敏感，必须严格遵循驼峰写法（如 `Math.ceil` 不能写成 `Math.Ceil`）。