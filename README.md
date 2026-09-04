# Imperseco Panama 项目说明

这是一套使用原生 HTML、CSS 和 JavaScript 制作的 Imperseco Panama 网站预览。

不需要安装 React、Vue 或数据库。用 VS Code 打开文件，修改后保存，再通过 Live Server 查看效果即可。

## 一、项目文件

```text
imperseco-preview/
├── index.html       首页，展示四个主题入口
├── sistema.html     主题详情的通用模板
├── roof.html        RoofShield 入口
├── wall.html        WallGuard 入口
├── interior.html    MoldBlock 入口
├── floor.html       FloorShield 入口
├── Imperseco-Panama.jpg  项目图片
└── README.md        本说明文件
```

### 页面是怎么连接的

首页的四张主题卡片分别链接到：

```html
roof.html
wall.html
interior.html
floor.html
```

这些入口文件会跳转到同一个详情模板，但传入不同的主题参数：

```text
sistema.html?modulo=roof
sistema.html?modulo=wall
sistema.html?modulo=interior
sistema.html?modulo=floor
```

`sistema.html` 中的 JavaScript 会读取 `modulo`，然后从 `systems` 数据对象中选择对应内容。因此，四个页面可以有不同内容，同时不用维护四份相同的页面结构。

## 二、如何用 Live Server 预览

1. 用 VS Code 打开整个 `imperseco-preview` 文件夹。
2. 在左侧文件列表中打开 `index.html`。
3. 右下角点击 **Go Live**。
4. 浏览器访问 Live Server 显示的地址，例如：

```text
http://127.0.0.1:5501/index.html
```

5. 在 VS Code 中修改代码。
6. 按 `Cmd + S` 保存。
7. 浏览器通常会自动刷新；没有刷新时按 `Cmd + R`。

建议打开 VS Code 的自动保存：

`Code` → `Settings` → 搜索 `Auto Save` → 选择 `afterDelay`

## 三、最简单的修改方法

### 1. 修改首页文字

打开 `index.html`，按 `Cmd + F` 搜索你想改的原文。例如：

```html
<h1>Una casa.<br>Cuatro superficies.<br><em>Una defensa completa.</em></h1>
```

可以修改文字，但建议保留 HTML 标签：

- `<br>`：换行
- `<em>...</em>`：应用强调样式
- `<p>...</p>`：段落
- `<h1>...</h1>`：主标题
- `<span>...</span>`：局部文字样式

例如：

```html
<h1>保护你的家。<br>从屋顶到地板。<br><em>完整防护。</em></h1>
```

### 2. 修改四个主题卡片文字

在 `index.html` 中搜索：

```text
01 / TECHO
```

对应的代码大致是：

```html
<h2>RoofShield<span>Impermeabilización + control térmico</span></h2>
<p>保护说明文字</p>
<a class="open" href="roof.html">VER SISTEMA <b>→</b></a>
```

可以修改：

- `<h2>`：主题名称
- `<span>`：主题副标题
- `<p>`：卡片说明
- `href="roof.html"`：点击后进入哪个页面

不要随便修改 `class="..."`，因为 CSS 通过 `class` 找到元素并控制样式。

### 3. 修改主题详情文字

打开 `sistema.html`，按 `Cmd + F` 搜索：

```text
const systems
```

里面有四组数据：

```javascript
const systems = {
  roof: { ... },
  wall: { ... },
  interior: { ... },
  floor: { ... }
};
```

每组里面常见的参数含义：

```javascript
{
  kicker: '01 / TECHO',
  title: 'RoofShield',
  intro: '页面顶部介绍',
  promise: '页面中间的大标题',
  description: '主题详细说明',
  tags: ['LLUVIA INTENSA', 'EXPOSICIÓN SOLAR'],
  hero: '图片地址',
  photo: '流程区域图片地址',
  use: '使用场景图片地址',
  useTitle: '使用场景标题',
  useCopy: '使用场景说明',
  steps: [ ... ]
}
```

修改文字时，只改引号里面的内容，保留参数名、冒号、逗号和括号。例如：

```javascript
title: '我的新主题',
intro: '这是我的主题介绍。',
```

### 4. 修改步骤

每个主题都有 `steps`，每一步由三个值组成：编号、标题、说明。

```javascript
steps: [
  ['01', 'Inspeccionar', '检查表面状况。'],
  ['02', 'Preparar', '清洁并准备基层。']
]
```

添加步骤时，复制一行并修改内容：

```javascript
['03', 'Aplicar', '按项目要求进行施工。'],
```

最后一行通常不要加逗号也可以，但保留逗号更容易继续添加内容。

## 四、如何更改图片

### 首页图片

打开 `index.html`，搜索：

```text
background:url(
```

四张主题卡片使用 CSS 背景图片，例如：

```css
.roof{background:url('图片地址') center/cover}
```

把引号中的地址替换成图片地址：

```css
.roof{background:url('https://example.com/roof.jpg') center/cover}
```

首页 Logo 使用：

```html
<img class="logo" src="imperseco-panama.jpg" alt="Imperseco Panamá">
```

如果使用本地图片，图片应放在项目文件夹内，并且文件名大小写必须完全一致。例如文件叫 `Imperseco-Panama.jpg`，代码里的 `src` 也必须写成同样的大小写。

### 详情页图片

打开 `sistema.html`，搜索 `hero:`、`photo:` 或 `use:`。例如：

```javascript
hero: 'https://example.com/roof-hero.jpg',
photo: 'https://example.com/roof-process.jpg',
use: 'https://example.com/roof-use.jpg',
```

三个图片参数分别用于：

- `hero`：详情页顶部大图
- `photo`：步骤区域图片
- `use`：使用场景图片

推荐图片格式：`.jpg`、`.jpeg`、`.png` 或 `.webp`。网上图片必须允许外链，否则 Live Server 中可能无法显示。

## 五、如何调整颜色、距离和字体

这些样式目前都写在每个 HTML 文件的 `<style>...</style>` 区域中。

### 修改主颜色

打开 `index.html` 或 `sistema.html`，搜索：

```css
:root{
```

你会看到类似：

```css
:root{
  --ink:#101817;
  --paper:#e8e6df;
  --orange:#e65c19;
}
```

这些是全局颜色变量：

- `--ink`：深色背景
- `--paper`：浅色背景或浅色文字
- `--orange`：橙色强调色
- `--line`：分隔线颜色

修改颜色时使用十六进制颜色，例如：

```css
--orange:#2d8cff;
```

### 修改横向卡片效果

在 `index.html` 搜索：

```css
.modules
```

四张卡片横向排列是因为：

```css
.modules{display:flex}
```

鼠标移入时卡片变宽是因为：

```css
.module:hover{flex:2.15}
```

如果不想让卡片移入时展开，可以删除这一条规则，或改成：

```css
.module:hover{flex:1}
```

### 修改页面距离

常见写法：

```css
padding: 80px 7vw;
margin: 20px 0;
gap: 60px;
```

- `padding`：元素内部距离
- `margin`：元素外部距离
- `gap`：网格或弹性布局项目之间的距离
- `px`：固定像素
- `vw`：根据浏览器宽度变化的单位
- `rem`：根据根字体大小变化的单位

例如：

```css
.hero{padding:120px 6vw 50px}
```

其中四个值依次是：上、右、下、左。如果只写两个值，则分别代表上下、左右：

```css
padding: 80px 7vw;
```

### 修改字体大小

搜索 `font-size`：

```css
font-size: 18px;
```

数字越大，文字越大。`clamp(...)` 是响应式字体写法，会根据屏幕宽度自动调整大小，建议新手先不要删除。

## 六、特殊符号和代码规则

### HTML 符号

```html
<!-- 这是注释，网页不会显示 -->
<br>                 <!-- 换行 -->
&amp;                 <!-- 显示 & -->
&quot;                <!-- 显示双引号 -->
```

### CSS 符号

```css
.class-name {       /* 选择 class */
  color: red;       /* 属性: 值; */
}
```

- `.` 开头表示 class，例如 `.hero`
- `#` 开头表示 id，例如 `#sistema`
- `:` 用于属性和值之间，也用于 `:hover`
- `{}` 包住一组 CSS 规则
- `;` 结束一条 CSS 属性
- `/* ... */` 是 CSS 注释

### JavaScript 符号

```javascript
const name = 'value';
```

- `const`：定义不会重新指向其他值的变量
- `=`：赋值
- `'文字'` 或 `"文字"`：字符串
- `[]`：数组，例如 `['A', 'B']`
- `{}`：对象或代码块
- `,`：分隔多个值
- `;`：一条语句结束
- `` `文字 ${name}` ``：可以插入变量的模板字符串

最重要的规则：修改数组或对象中的一项时，要注意上一项后面的逗号，且不要误删成对的括号。

## 七、如何创建新的主题页面

### 推荐方式：复用现有模板

如果要增加第五个主题，推荐继续使用 `sistema.html`，不需要复制整份 HTML。

1. 在 `sistema.html` 的 `systems` 对象中添加一组数据：

```javascript
newtopic: {
  kicker: '05 / NUEVO',
  title: 'NewTopic',
  intro: '新主题介绍。',
  promise: '新主题的大标题。',
  description: '新主题的详细说明。',
  tags: ['标签一', '标签二'],
  hero: 'https://example.com/hero.jpg',
  photo: 'https://example.com/process.jpg',
  use: 'https://example.com/use.jpg',
  useTitle: '使用场景标题。',
  useCopy: '使用场景说明。',
  steps: [
    ['01', '第一步', '第一步说明。'],
    ['02', '第二步', '第二步说明。']
  ]
}
```

2. 在 `index.html` 增加一个入口链接：

```html
<a class="open" href="sistema.html?modulo=newtopic">VER SISTEMA <b>→</b></a>
```

这样可以先正常进入详情页。

### 如果需要独立文件名

也可以创建 `newtopic.html`，内容结构参考现有的 `roof.html`：

```html
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta http-equiv="refresh" content="0; url=sistema.html?modulo=newtopic">
  <title>Imperseco — NewTopic</title>
</head>
<body>
  <p>Redirigiendo...</p>
  <script>location.replace('sistema.html?modulo=newtopic');</script>
</body>
</html>
```

然后首页链接改为：

```html
<a class="open" href="newtopic.html">VER SISTEMA <b>→</b></a>
```

### 什么时候才需要复制一份完整 HTML

只有当新页面的结构完全不同，例如需要完全不同的导航、布局、表单或交互时，才建议复制 `sistema.html` 并单独改造。普通主题只需要增加数据，不需要复制模板。

## 八、修改后检查什么

每次修改后按这个顺序检查：

1. VS Code 是否显示红色错误提示。
2. 浏览器是否能打开页面。
3. 页面文字是否正常显示。
4. 图片是否能加载。
5. 点击按钮是否进入正确页面。
6. 浏览器开发者工具中是否出现错误。

常见问题：

- 页面空白：通常是 JavaScript 少了引号、逗号或括号。
- 图片不显示：检查图片地址、文件名和大小写。
- 点击无反应：检查 `href` 是否拼写正确。
- 5500 端口 404：确认 Live Server 显示的实际端口，有时是 `5501`。
- 修改没有变化：确认已经按 `Cmd + S` 保存，并刷新浏览器。

## 九、以后如何继续维护这份 README

你之后可以继续问我具体问题，例如：

- “我想把首页橙色改成蓝色，应该改哪里？”
- “我想增加一个卫生间主题，帮我接入现有结构。”
- “我改完以后页面空白，帮我找错误。”
- “我想让手机端卡片更高，应该调整什么？”

我可以根据当前项目检查代码，给你明确的修改位置，也可以直接帮你修改文件。确认过的问答还可以继续追加到本 README，逐渐变成这套项目专属的操作手册。

## 十、给新手的安全编辑习惯

- 修改前先保存一份备份。
- 一次只改一个小地方，保存后马上预览。
- 不要一次删除大量代码。
- 修改文字时尽量只改引号里面的内容。
- 修改 CSS 时保留 `{`、`}`、`;` 和成对的引号。
- 不确定某一段代码用途时，先搜索它的 `class`、`id` 或参数名称，再进行修改。
