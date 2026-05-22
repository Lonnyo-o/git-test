# git-test
# CSS 常用属性大全（完整版）
> 前端开发必备速查表 | 按功能分类整理 | 包含属性说明、常用取值和使用场景
> 可直接复制保存为 `CSS常用属性大全.md` 文件本地查阅

---

## 一、文本样式
控制文字颜色、大小、对齐、粗细、装饰等基础样式
```css
/* 文字颜色 */
color: 颜色值; /* 支持英文/十六进制/RGB/HSL，例：red、#fff、rgb(0,0,0) */

/* 文字大小 */
font-size: 16px; /* 常用单位：px、rem、em、% */

/* 文字粗细 */
font-weight: normal;  /* 正常（400） */
font-weight: bold;    /* 加粗（700） */
font-weight: 100-900; /* 数值精细控制 */

/* 文字水平对齐 */
text-align: left;     /* 左对齐（默认） */
text-align: center;   /* 居中 */
text-align: right;    /* 右对齐 */
text-align: justify;  /* 两端对齐 */

/* 文字装饰 */
text-decoration: none;        /* 清除装饰（常用清除a标签下划线） */
text-decoration: underline;   /* 下划线 */
text-decoration: line-through;/* 删除线 */

/* 行高（控制文字垂直间距） */
line-height: 1.5; /* 无单位=倍数，推荐 1.4~1.8 */

/* 文字字体 */
font-family: "微软雅黑", sans-serif; /* 优先字体, 备用字体 */

/* 单行文字溢出省略（必备） */
white-space: nowrap;   /* 强制不换行 */
overflow: hidden;      /* 溢出隐藏 */
text-overflow: ellipsis;/* 溢出显示... */
```

##  二、背景样式 
```css
/* 背景纯色 */
background-color: 颜色值;

/* 背景图片 */
background-image: url(图片路径);

/* 背景重复方式 */
background-repeat: no-repeat; /* 不重复 */
background-repeat: repeat-x;  /* 横向重复 */
background-repeat: repeat-y;  /* 纵向重复 */

/* 背景位置 */
background-position: center;   /* 居中 */
background-position: left top; /* 左上角 */

/* 背景大小 */
background-size: cover;   /* 铺满容器（自动裁剪） */
background-size: contain; /* 完整显示（不裁剪） */
background-size: 100% 100%;/* 拉伸铺满 */

/* 背景简写（推荐使用） */
background: 颜色 图片 重复 位置 / 大小;
/* 示例：background: #fff url(xxx.png) no-repeat center / cover; */
```

## 三、盒子模型（布局核心）

控制元素的宽高、内边距、边框、外边距，是所有布局的基础

```css
/* 元素宽高 */
width: 200px;        /* 宽度 */
height: 100px;       /* 高度 */
max-width: 100%;     /* 最大宽度（自适应常用） */
min-height: 100vh;   /* 最小高度满屏 */

/* 内边距（内容→边框的距离） */
padding: 10px;          /* 上下左右统一 */
padding: 10px 20px;     /* 上下 | 左右 */
padding: 5px 10px 15px; /* 上 | 左右 | 下 */
padding: 1px 2px 3px 4px;/* 上 → 右 → 下 → 左 */

/* 边框 */
border: 1px solid #ccc; /* 宽度 | 样式 | 颜色 */
border-radius: 4px;     /* 圆角 */
border-radius: 50%;     /* 圆形（宽高一致时） */

/* 外边距（元素→元素的距离） */
margin: 10px;        /* 上下左右统一 */
margin: 0 auto;      /* 块级元素水平居中 */

/* 盒子模型规则（必加，防止撑大元素） */
box-sizing: border-box; /* 宽高包含边框+内边距 */
```

## 四、Flex 弹性布局

现代布局首选，轻松实现居中、均匀分布、自适应排列

```css
/* 父元素：开启弹性布局 */
display: flex;

/* 子元素排列方向 */
flex-direction: row;     /* 横向排列（默认） */
flex-direction: column;  /* 纵向排列 */

/* 子元素水平对齐 */
justify-content: flex-start;    /* 左/上（默认） */
justify-content: center;        /* 水平居中 */
justify-content: space-between; /* 两端对齐，无间距 */
justify-content: space-around;  /* 均匀分布，有间距 */

/* 子元素垂直对齐 */
align-items: center;     /* 垂直居中 */
align-items: flex-start; /* 顶部对齐 */
align-items: flex-end;   /* 底部对齐 */

/* 子元素自动换行 */
flex-wrap: wrap; /* 自动换行 */

/* 子元素：占比分配 */
flex: 1; /* 平分剩余空间 */
```

## 五、定位属性

用于悬浮、固定、吸附、层级覆盖等特殊布局

```css
/* 定位类型 */
position: relative; /* 相对定位（不脱离文档流，参考自身） */
position: absolute; /* 绝对定位（脱离文档流，参考最近定位父级） */
position: fixed;    /* 固定定位（悬浮屏幕，不随滚动变化） */
position: sticky;   /* 粘性定位（滚动到顶部自动吸附） */

/* 位置偏移（配合定位使用） */
top: 0;    /* 距离顶部 */
right: 0;  /* 距离右侧 */
bottom: 0; /* 距离底部 */
left: 0;   /* 距离左侧 */

/* 层级控制（数值越大越在上层） */
z-index: 999;
```

## 六、元素显示与隐藏

三种常用隐藏方式，效果和占用空间不同

```css
display: none;      /* 完全隐藏，不占用空间，无法交互 */
visibility: hidden; /* 视觉隐藏，占用空间，无法交互 */
opacity: 0;         /* 透明隐藏，占用空间，可交互 */
opacity: 1;         /* 正常显示 */
```

## 七、浮动与清除浮动 

 传统布局方式，用于元素横向排列 

```css
/* 浮动 */
float: left;  /* 左浮动 */
float: right; /* 右浮动 */

/* 清除浮动（解决父元素高度塌陷） */
clear: both;

/* 万能清除浮动类（直接复用） */
.clearfix::after {
  content: "";
  display: block;
  clear: both;
  visibility: hidden;
  height: 0;
}
```

## 八、阴影与透明度

增强元素视觉效果，常用在卡片、按钮、文字强调

```css
/* 盒子阴影 */
box-shadow: 水平偏移 垂直偏移 模糊度 颜色;
/* 示例：box-shadow: 0 2px 10px rgba(0,0,0,0.1); */

/* 文字阴影 */
text-shadow: 1px 1px 2px #000;

/* 整体透明度 */
opacity: 0~1; /* 0完全透明，1不透明 */
```

## 九、鼠标样式

定义鼠标悬浮在元素上的光标样式

```css
cursor: pointer;  /* 小手（可点击，最常用） */
cursor: default;  /* 默认箭头 */
cursor: text;     /* 文字输入光标 */
cursor: move;     /* 移动十字光标 */
cursor: not-allowed; /* 禁止图标 */
```

## 十、过渡与动画

实现元素平滑变化、动态交互效果

```css
/* 过渡（hover变化平滑） */
transition: 变化属性 时长 速度曲线;
/* 示例：transition: all 0.3s ease; 所有属性0.3秒平滑变化 */

/* 动画（自定义动态效果） */
animation: 动画名称 时长 循环次数;
/* 示例：animation: move 1s infinite; 无限循环动画 */
```
