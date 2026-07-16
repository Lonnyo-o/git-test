# JSON 对象 学习笔记

## 一、JSON 简介
1. JSON（JavaScript Object Notation）是一种**轻量级的数据交换格式**，专门用于数据的存储与跨端传输。
2. 在 JavaScript 中，`JSON` 是内置全局对象，封装了对 JSON 格式数据的解析与生成方法。
3. JSON 本质是纯文本字符串，与编程语言无关，所有主流开发语言都支持读取和生成 JSON 格式数据。

## 二、JSON 的作用
核心用途是**前后端数据交互**：服务端向网页传递数据时，通常以 JSON 字符串格式传输；前端接收到后，解析为 JS 对象/数组再进行业务操作。

## 三、JSON 的两种基础结构
JSON 只有两种基础结构：对象、数组，二者可任意嵌套组合。

### 1. JSON 对象
语法格式：`{"键名": "值", "键名": "值"}`
- 核心语法规则：
  - 键名必须用**双引号**包裹（JS 对象的键可以不加引号/用单引号，JSON 语法不允许）
  - 字符串类型的值必须用双引号包裹
  - 键值对之间用逗号分隔，**最后一个键值对末尾不能加逗号**

### 2. JSON 数组
语法格式：`[元素1, 元素2, 元素3]`
- 数组元素可以是对象、字符串、数字、布尔值等合法 JSON 类型
- 开发中最常用的是**对象数组**：`[{}, {}, {}]`

> ❗ 纠错说明：原笔记此处混入了 `new Array()` 等 JS 数组创建的代码，属于知识点错位。数组创建是 JS 基础语法，不属于 JSON 结构的范畴，已移除。

## 四、JSON 与字符串的相互转换
数据传输时使用 **JSON 字符串**，JS 代码中操作的是 **JS 对象/数组**，两种格式的互转是开发核心操作。

### 1. 序列化：JS 对象/数组 → JSON 字符串
语法：`JSON.stringify(待转换的JS对象/数组)`
- 返回值：符合 JSON 语法规范的纯字符串

### 2. 反序列化：JSON 字符串 → JS 对象/数组
共有两种实现方式，推荐优先使用 `JSON.parse`

| 方法 | 语法 | 说明 |
|------|------|------|
| `JSON.parse()` | `JSON.parse(json字符串)` | 官方标准方法，仅解析合法 JSON 格式，安全可靠，开发推荐使用 |
| `eval()` | `eval('(' + json字符串 + ')')` | 可执行任意 JS 代码，存在**代码注入安全风险**，不推荐生产环境使用 |

> 补充：为什么 eval 要包裹括号？
> 当 JSON 以 `{` 开头时，JS 会将其识别为代码块而非对象字面量；外层包裹括号后，会强制 JS 将其解析为表达式，从而正确得到对象。

## 五、完整实操案例
### 案例1：JSON 对象的基础读写
```javascript
// 定义符合JSON格式的JS对象
var obj = {"name":"张三", "sex":"男", "age":"18"};

// 取值：两种语法
console.log(obj.name);    // 点语法，输出：张三
console.log(obj["name"]); // 中括号语法，输出：张三

// 修改属性值
obj.name = "李四";
console.log(obj.name); // 输出：李四
```

### 案例2：JSON 对象数组的基础读写
```javascript
// 定义对象数组（最常用的JSON结构）
var arr = [
    {"name":"张三", "sex":"男", "age":"18"},
    {"name":"李思", "sex":"男", "age":"38"},
    {"name":"刘静", "sex":"女", "age":"9"}
];

// 输出完整数组
console.log(arr);

// 取出数组第2个元素的sex属性（数组下标从0开始计数）
console.log(arr[1].sex); // 输出：男

// 修改指定元素的属性
arr[1].sex = "女";
console.log(arr[1].sex); // 输出：女
```

### 案例3：序列化（对象/数组 → JSON字符串）
```javascript
var obj = {"name":"张三", "sex":"男", "age":"18"};
var arr = [
    {"name":"张三", "sex":"男", "age":"18"},
    {"name":"李思", "sex":"男", "age":"38"}
];

// 打印原数据（JS对象/数组类型）
console.log(obj);
console.log(arr);

// 转为JSON字符串
var objStr = JSON.stringify(obj);
var arrStr = JSON.stringify(arr);

console.log(objStr); // 输出：'{"name":"张三","sex":"男","age":"18"}'
console.log(arrStr); // 输出数组格式的JSON字符串
```

### 案例4：反序列化（JSON字符串 → 对象/数组）
```javascript
// 1. 解析对象格式的JSON字符串
var str1 = '{"name":"张三","sex":"男","age":"18"}';

// 推荐方式：JSON.parse
var obj1 = JSON.parse(str1);
console.log(obj1);          // 输出完整JS对象
console.log(obj1.sex);      // 输出：男

// 不推荐方式：eval
var obj2 = eval("(" + str1 + ")");
console.log(obj2);


// 2. 解析数组格式的JSON字符串
var str2 = '[{"name":"张三","sex":"男","age":"18"},{"name":"张三1","sex":"男","age":"18"},{"name":"张三2","sex":"男","age":"18"}]';

var arr = JSON.parse(str2);
console.log(arr);

// eval方式解析数组
var arr2 = eval("(" + str2 + ")");
console.log(arr2);
```

## 六、补充：JSON 语法易错点与注意事项
1. **强制双引号**：键名、字符串值必须使用双引号，单引号、无引号都会导致 `JSON.parse` 解析失败
   - 错误写法：`{'name':'张三'}`、`{name:"张三"}`
   - 正确写法：`{"name":"张三"}`
2. 不支持注释：JSON 中不能写 `//` 或 `/* */` 注释
3. 禁止尾随逗号：最后一个键值对/数组元素末尾不能加逗号
4. 支持的值类型：字符串、数字、布尔值、`null`、对象、数组；**不支持**函数、`undefined`、Symbol 类型
5. 异常处理：`JSON.parse()` 遇到非法 JSON 字符串会直接报错，生产环境建议用 `try-catch` 包裹捕获异常

需要我补充 JSON.parse 异常处理和 JSON 实现深拷贝的扩展案例吗？