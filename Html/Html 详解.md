# Html 详解

> Html5更新

### 1. 什么是HTML

​	Hyper Text Markup Language(超文本标记语言)

   **W3C标准**：

- 结构化标准语言(HTML、XML)
- 表现标准语言(CSS)
- 行为标准(DOM、ECMAScript)

### 2. 网页基本结构

##### 1) <!DOCTYPE> 

​	使用什么规范，默认为html

##### 2) head、meta、title

​	网页头部、描述性标签、网页标题

```html
<!-- Html注释结构 -->
<!-- 单组标签称为单闭合标签，<></>称为开放、闭合标签 -->
<meta name = "keywords" content="网页关键字"/>
```

##### 3) body、header、footer、section、nav

​	网页主体

### 3. 网页基本标签元素-更至Html5标准

##### 标题标签：<p></p>

##### 段落标签：<h1>

##### 块元素与行内标签：<div> 

##### 换行标签：<br/>

##### 水平线标签：<hr></hr>

##### 粗体、斜体：<Strong></Strong> <em></em>

空格、大于、小于、其他特殊符号 &nbsp

##### 图像标签：

- 在大标签<img>中，可包含其他属性
- 必填项：src：图片路径(相对 绝对)    alt：替代文本
- title：鼠标悬停文本 
- width height

##### 超链接标签(已更新)

​	<a></a>

###### 	相关属性：

- name：作为标记，帮助锚链接跳转 

- id：创建一个 HTML 文档书签

  ```html
  <a id="tips">有用的提示部分</a>
  <a href="#tips">访问有用的提示部分</a>
  <a href="https://www.runoob.com/html/html-links.html#tips">
  ```

- <u>href</u>：链接跳转URL，在 HTML5 中，<a> 标签是超链接，但是假如没有 href 属性，它仅仅是超链接的一个占位符。

- 功能性链接：

  - QQ链接(QQ推广)
  

######    html5 新属性 ：

- download：指定下载链接

  ```html
  <a href="...." download="./download1.png"></a>
  ```

- media：需要href，规定目标 URL 的媒介类型(是为什么类型的媒介/设备进行优化的)

  运算符： and / not /,

  运行设备： all / screen / print / tv /...

  值：宽、高、像素比...

  ```html
  <a href="...." media="print and (width:300px)"></a>
  ```

- rel：需要href，规定当前文档与目标 URL 之间的关系

  | 值       | 描述                                                         |
  | -------- | ------------------------------------------------------------ |
  | contents | 文档目录。                                                   |
  | index    | 文档索引。                                                   |
  | nofollow | Google 使用 "nofollow"，用于指定 Google 搜索引擎不要跟踪链接。作用：降低权重，减少恶意骚扰，精准查找 |

- target：需要href，规定在何处打开目标 URL

  | 值          | 描述                                 |
  | ----------- | ------------------------------------ |
  | _blank      | 在新窗口中打开被链接文档。           |
  | _self       | 默认。在相同的框架中打开被链接文档。 |
  | _parent     | 在父框架集中打开被链接文档。         |
  | _top        | 在整个窗口中打开被链接文档。         |
  | *framename* | 在指定的框架中打开被链接文档。       |

  ```html
  <a href="www.baidu.com" target="_blank"></a>
  ```
  
- type：需要href，规定目标 URL 的 MIME (媒体类型)类型,例如：`text/plain` 、 `text/html`等

  ```html
  <a href="www.baidu.com" type="text/html"></a>
  ```

##### 列表(已更新)

​	<ol> <ul> <li>  无序，有序，列表项

​	<dl><dt><dd>    描述列表，项目/名字

##### 表单(已更新)

​	<form></form> 收集用户在此区域的不同输入

###### 相关属性：

- <u>method</u>：提交方式 (get 【将表单数据追加到 URL】 / post 【将表单数据附加在 HTTP 请求的正文中】)
- <u>action</u>： 提交表单时要执行的操作
- target：上同
- placeholder 、required、pattern：默认提示，不为空，正则表达式

######  html5 新属性：

在与input标签一起使用时：

- autocomplete = "on/off" ：属性规定表单或输入字段是否应该自动完成(记录用户输入过的值)
- novalidate：规定在提交表单时不对表单数据进行验证
- autofocus：布尔属性，是否自动聚焦
- form+标签(action/enctype/method/validate/target)：覆盖form中的属性

######  相关标签：

**下拉框** <select></select>  ---> **下拉框选项** <option></option> ---> **父级分类** <optgroup label=""></optgroup>

**文本域** <textarea></textarea>

**标签** <label></label>

**按钮** <button></button>		拥有属性：disabled / form / name / type 

**表单增强效果** <fieldset></fieldset> ---> **标题** <legend></legend>

##### **输入框**(已更新)

​	<input/> 多数情况下与表单一起使用

###### 相关属性：

- type：输入框的类型

  | 类型名称 | 作用 | 类型名称 | 作用  |
  | ----- | ----- | ----- | ----- |
  | text   | 文本域 | password | 密码 |
  | button | 默认按钮 | radio | 单选按钮 |
  | submit | 提交按钮 | checkbox | 复选框（通过name定义组） |
  | reset                                | 重置按钮 | image | 图片 |
  | -----html5新增类型，老式默认变为text | | | |
  | number  **强化属性--->step** | 数字   | 详情：拥有输入限制 |[disabled,min,max,required,readonly....]|
  | date/month/week/time/datetime | 时间 | color | 颜色 |
  | range | 滑块 | search | 搜索字段 |
  | url | URL 地址 | file               | 文件域 |
  
- value：默认值

- readonly 、disabled、size、maxlength：只读，禁用，尺寸，最大长度

######  html5 新属性：

- list ：属性规定输入域的 datalist，datalist 是输入域的选项列表。
- placeholder 、required、pattern：默认提示，不为空，正则表达式
- multpie：boolean 属性，属性规定<input> 元素中可选择多个值



##### 表格(已更新)

​	<table></table> 

###### 相关标签:

| 名称                  | 作用                        | 名称       | 作用                 |
| --------------------- | --------------------------- | ---------- | -------------------- |
| <tr>                  | 表格行                      | <col>      | 表格列               |
| <td>                  | 单元格                      | <colgroup> | 表格列组             |
| <th>                  | 表头                        | <caption>  | 标题，一般放在最前头 |
| <thead><tbody><tfoot> | 页眉，主体，页脚，与Css使用 |            |                      |

###### 相关属性：

​	**注意**：这里只写了H5有的相关的属性，表格主要由Css控制

- border：表格边框
- colespan/rolespan ：规定表头可横跨的列、行数
- span：规定 <col> 元素应该横跨的列数

##### 视频和音频

##### iframe 内联框架：

- 在大标签<iframe>中，可包含其他属性

- 必填项：src：地址

- name: target所传递的位置

- width height

  

### 4.Html5新特性

##### data-* 属性：

嵌入自定义数据：

```html
<ul>
<li data-animal-type="鸟类">喜鹊</li>
<li data-animal-type="鱼类">金枪鱼</li> 
<li data-animal-type="蜘蛛">蝇虎</li> 
</ul>
```

##### contextmenu 属性：

规定 <div> 元素的上下文菜单。上下文菜单会在用户右键点击元素时出现：

```html
<div contextmenu="mymenu">

<menu type="context" id="mymenu">
  <menuitem label="Refresh"></menuitem>
  <menuitem label="Twitter"></menuitem>
</menu>

</div>	
```

##### contenteditable 属性:

一段可编辑的段落：

```html
<p contenteditable="true">这是一个可编辑的段落。</p>
```

