[TOC]

# Bootstrap学习

## 排版

### small

被用来制作副标题

> <h1>Bootstrap标题<small>我是副标题</small></h1>

### 文本强调相关的类

| 强调类           | 意思        |
| ------------- | --------- |
| .text-muted   | 提示（浅灰色）   |
| .text-primary | 主要（蓝色）    |
| .text-success | 成功（浅绿色）   |
| .text-info    | 通知信息（浅蓝色） |
| .text-warning | 警告（黄色）    |
| .text-danger  | 危险（褐色）    |

### text-justify

文本两端对齐，段落两段对齐没有空格



### 定义列表dl和dt、dd

```html
<dl>
  <dt>定义列表标题</dt>
  <dd>定义列表信息1</dd>
  <dd>定义列表信息2</dd>
</dl>
```



### 去点列表

`.list-unstyled`去除默认的列表样式的风格



### 内联列表

`.list-inline` 把垂直列表换成水平列表，而且去掉项目符号,保持水平显示



### 水平定义列表

给`<dl>`添加类名`.dl-horizontal`给定义列表实现水平显示效果

只有屏幕大于*768px*的时候，才有效果，其实现主要方式

1. **将dt设置了一个左浮动，并且设置了一个宽度为160px**
2. **将dd设置一个margin-left的值为180px，达到水平的效果**
3. **当标题宽度超过160px时，将会显示三个省略号**



### 表格

| 类名               | 表格样式      |
| ---------------- | --------- |
| .table           | 基础表格      |
| .table-striped   | 斑马线的表格    |
| .table-bordered  | 带边框的表格    |
| .table-hover     | 鼠标悬停高亮的表格 |
| .table-condensed | 紧凑型表格     |
| .table-reponsive | 响应式       |

**相应式表格**

当你的浏览器可视区域小于**768px**时，表格底部会出现水平滚动条。当你的浏览器可视区域大于768px时，表格底部水平滚动条就会消失。

```html
<div class="table-responsive">  <!--给容器添加类名-->
<table class="table table-bordered">
   …
</table>
</div>
```



### 表格行的类(tr)

| 类名        | 描述               |
| --------- | ---------------- |
| .active   | 悬停在行或单元格上时所设置的颜色 |
| .scuccess | 成功或者正确的行为        |
| .info     | 普通的提示信息或动作       |
| .warning  | 警告或需要用户注意        |
| .danger   | 危险或潜在的带来负面影响的动作  |



### 基础表格

```html
<table class="table">
  <thead>
  	<tr>
    	<th>表格标题</th>
        <th>表格标题</th>
        <th>表格标题</th>
    </tr>
  </thead>
  <tbody>
  	<tr>
   		<td>表格单元格</td>
        <td>表格单元格</td>
        <td>表格单元格</td>
    </tr>
    <tr>
   		<td>表格单元格</td>
        <td>表格单元格</td>
        <td>表格单元格</td>
    </tr>
  </tbody>
</table>
```





## 表单

### .form-control

设置此类的<input>、<textarea>和<select>元素

**1、宽度变成了100%**

**2、设置了一个浅灰色（#ccc）的边框**

**3、具有4px的圆角**

**4、设置阴影效果，并且元素得到焦点之时，阴影和边框效果会有所变化**

**5、设置了placeholder的颜色为#999**

