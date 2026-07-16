# JS Date 日期对象核心方法笔记（修正+补充版）
> 统一调用格式：`日期对象.方法名()`，所有 `get` 系列方法都是「从日期里取出对应部分」

## 预备：创建日期对象的4种常用写法
```js
// 1. 获取当前系统时间（最常用）
var d1 = new Date();

// 2. 用数字构造（年,月,日,时,分,秒）⚠️ 月份从0开始，8月写7
var d2 = new Date(2008, 7, 22, 14, 7, 30); 

// 3. 用标准字符串构造（推荐用横杠分隔，兼容性最好）
var d3 = new Date("2008-08-22 14:07:30");

// 4. 用时间戳还原日期
var d4 = new Date(1225344450000);
```
> ❌ 原笔记错误修正：不推荐 `new Date("2008.8.22")` 点分隔格式，它不是JS标准日期写法，部分浏览器会解析失败，变成无效日期。

---

## 一、核心 get 系列方法
### 1. getFullYear() — 获取完整年份
- **作用**：取出日期里完整的4位年份
- **返回值**：4位整数（如 2026、2008）

```js
// 例子1：获取今年的年份
var now = new Date();
console.log(now.getFullYear()); 
// 输出当前年份，例如 2026

// 例子2：获取指定日期的年份
var birthday = new Date(2008, 7, 22);
console.log(birthday.getFullYear()); 
// 输出：2008
```
- 注意：永远用这个方法。废弃的老方法 `getYear()` 有千年虫bug，禁止使用。

---

### 2. getMonth() — 获取月份
- **作用**：取出日期对应的月份
- **返回值**：0 ~ 11 的整数
  - 0 = 1月，1 = 2月，...，7 = 8月，...，11 = 12月

```js
// 例子1：获取当前月份
var now = new Date();
console.log(now.getMonth()); 
// 比如7月会输出 6

// 例子2：获取指定日期的月份
var birthday = new Date(2008, 7, 22); // 构造的是2008年8月22日
console.log(birthday.getMonth()); 
// 输出：7

// 例子3：日常使用要 +1 才是我们习惯的月份
var realMonth = birthday.getMonth() + 1;
console.log(realMonth); 
// 输出：8
```
- ⚠️ 原笔记错误修正：8月对应的返回值是7，不是8；返回8代表9月。同时构造日期时月份参数也要遵循从0计数的规则。
- 经典坑点：不管是「读取月份」还是「用数字构造日期」，月份都是从0开始计数。

---

### 3. getDate() — 获取当月几号
- **作用**：取出日期是当月的第几天（几号）
- **返回值**：1 ~ 31 的整数

```js
// 例子1：获取今天是几号
var now = new Date();
console.log(now.getDate()); 
// 比如2号就输出 2

// 例子2：获取指定日期是几号
var birthday = new Date("2008-08-22");
console.log(birthday.getDate()); 
// 输出：22

// 例子3：月末日期自动进位
var endMonth = new Date(2026, 1, 30); // 2月写30号，自动变成3月2号
console.log(endMonth.getDate()); 
// 输出：2
```
- 注意：别和 `getDay()` 搞混，这个是「几号」，不是星期几。

---

### 4. getDay() — 获取星期几
- **作用**：取出日期是星期几
- **返回值**：0 ~ 6 的整数
  - 0 = 星期日，1 = 星期一，...，6 = 星期六

```js
// 例子1：获取今天星期几
var now = new Date();
console.log(now.getDay()); 
// 比如周三输出 3，周日输出 0

// 例子2：获取指定日期的星期
var nationalDay = new Date("2019-10-01");
console.log(nationalDay.getDay()); 
// 输出：2（2019年10月1日是周二）

// 例子3：转成中文星期
var weekArr = ["日","一","二","三","四","五","六"];
console.log("星期" + weekArr[now.getDay()]);
// 输出类似：星期三
```
- ⚠️ 坑点：0 代表星期日，不是星期一。

---

### 5. getHours() — 获取小时
- **作用**：取出日期的小时数（24小时制）
- **返回值**：0 ~ 23 的整数

```js
// 例子1：获取当前小时
var now = new Date();
console.log(now.getHours()); 
// 比如下午2点输出 14，凌晨1点输出 1

// 例子2：获取指定时间的小时
var time = new Date(2008, 7, 22, 9, 30);
console.log(time.getHours()); 
// 输出：9

// 例子3：零点的返回值
var midnight = new Date("2026-07-02 00:00:00");
console.log(midnight.getHours()); 
// 输出：0
```

---

### 6. getMinutes() — 获取分钟
- **作用**：取出日期的分钟数
- **返回值**：0 ~ 59 的整数

```js
// 例子1：获取当前分钟
var now = new Date();
console.log(now.getMinutes()); 
// 比如10点25分输出 25

// 例子2：获取指定时间的分钟
var time = new Date("2008-08-22 14:07:30");
console.log(time.getMinutes()); 
// 输出：7
```

---

### 7. getSeconds() — 获取秒数
- **作用**：取出日期的秒数
- **返回值**：0 ~ 59 的整数

```js
// 例子1：获取当前秒数
var now = new Date();
console.log(now.getSeconds()); 
// 比如输出 30

// 例子2：获取指定时间的秒数
var time = new Date(2008, 7, 22, 14, 7, 30);
console.log(time.getSeconds()); 
// 输出：30
```

---

### 8. getTime() — 获取毫秒时间戳
- **作用**：返回从 **1970年1月1日 00:00:00（UTC时间）** 到该日期的总毫秒数
- **返回值**：十几位的大整数（时间戳），全球同一时刻值相同

```js
// 例子1：获取当前时间的时间戳
var now = new Date();
console.log(now.getTime()); 
// 输出类似 1783027200000

// 例子2：获取指定日期的时间戳
var birthday = new Date(2008, 7, 22);
console.log(birthday.getTime()); 
// 输出：1219324800000

// 例子3：简写写法（效果完全一样）
console.log(+new Date());
```
- 常用场景：计算时间差、对比两个时间的先后、生成简单唯一标识。

---

## 二、格式化方法补充
### 1. toLocaleString() — 完整本地化时间
- 作用：把日期转成「年月日 时分秒」的本地格式字符串
```js
var now = new Date();
console.log(now.toLocaleString());
// 输出类似：2026/7/2 14:30:45
```

### 2. toLocaleDateString() — 仅日期部分
```js
var now = new Date();
console.log(now.toLocaleDateString());
// 输出类似：2026/7/2
```

### 3. toLocaleTimeString() — 仅时间部分
```js
var now = new Date();
console.log(now.toLocaleTimeString());
// 输出类似：14:30:45
```

---

## 三、易错点总整理（必记）
1. **月份从0开始**：`getMonth()` 返回值、`new Date(年,月,日)` 构造时的月份参数，都遵循0=1月的规则，日常展示记得+1。
2. **getDate 和 getDay 别搞混**：
   - `getDate()` → 几号（1-31）
   - `getDay()` → 星期几（0-6，0是周日）
3. **日期字符串格式**：优先用 `YYYY-MM-DD` 横杠格式，点分隔、自定义斜杠格式在不同浏览器可能解析不一致。
4. **无效日期**：如果日期解析失败（比如乱写的字符串），所有 get 方法都会返回 `NaN`。
5. **时区问题**：所有 get 方法默认按本地时区计算；如果需要统一的UTC标准时间，用对应的 `getUTCFullYear()`、`getUTCMonth()` 等方法。