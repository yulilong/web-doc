## input介绍    

HTML`<input>`元素用于为基于Web的表单创建交互式控件，以便接受来自用户的数据。    

| 名称       | 介绍         |
|----------:|:--------------|
| 内容分类    | 流动区域; 内容区域; 交互式内容（如果不是处于隐藏状态）; 列表，可标签，可提交，可重置，与表单相关的元素。 |
| 允许的内容  | 无，这是一个void元素 |
| 标签省略    | 必须有开始标签。在 HTML 中，`<input>`标签没有结束标签。单标签中`/`可省略。在 XHTML 中，`<input>`标签必须被正确地关闭。|       

***注：什么是内容？***   
```
<!-- hello就是内容 -->
<div>hello</div>
<!-- 这个就是内容可以为空的标签 -->
<input type="text">
```



## input的属性介绍   

input元素支持[全局属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes)，以及以下属性。     

<table>
    <tr>
        <th>属性</th>
        <th>值</th>
        <th>描述</th>
    </tr>
    <tr>
        <td>type </td>
        <td>
          text  <br>
          password  <br>
          button  <br>
          radio   <br>
          checkbox   <br>
          file   <br>
          hidden   <br>
          image   <br>
          reset   <br>
          submit   <br>
          HTML5新增：  <br>
          date   <br>
          datetime   <br>
          datetime-local  <br>
          time    <br>
          week    <br>
          month    <br>
          color    <br>
          email    <br>
          number    <br>
          range    <br>
          tel <br>
          url <br>
          search <br>
        </td>
        <td>规定 input 元素的类型，如果这个属性没有指定，默认的类型是 text。</td>
    </tr>
    <tr>
      <td>accept</td>
      <td>
        1. 以 STOP 字符 (U+002E) 开始的文件扩展名。（例如：".jpg,.png,.doc"） <br>
        一个有效的 MIME 类型 <br>
        HTML5新增：  <br>
        2. `audio/*`音频文件 <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"> <br>
        3. `video/*`视频文件 <img src="https://github.com/yulilong/web-doc/blob/master/img/HTML5-icon.jpg" height="15px"> <br>
        4. `image/*`图片文件 <img src="http://p1ibqa9uh.bkt.clouddn.com/18-1-18/22359500.jpg" height="15px"> <br>
      </td>
      <td>如果该元素的 type 属性的值是file,则该属性表明了服务器端可接受的文件类型；否则它将被忽略。该属性的值必须为一个逗号分割的列表,包含了多个唯一的内容类型声明</td>
    </tr>
  </table> 



| 名称      | 介绍           |
|----------|:---------------|
| type     | input控件类型的显示。如果这个属性没有指定，默认的类型是 text。 |


### type   

控件类型的显示。如果这个属性没有指定，默认的类型是 text。可用的值包括：   

之前的值：    

| 名字      | 作用           |
|----------|:--------------|
| text      | 单行字段；换行会将自动从输入的值中移除。  | 
| password  | 一个值被遮盖的单行文本字段。使用 maxlength 指定可以输入的值的最大长度 。  |
| button    | 定义可点击按钮（多数情况下，用于通过 JavaScript 启动脚本） |
| radio     | 单选按钮。必须使用 value 属性定义此控件被提交时的值。使用checked 必须指示控件是否缺省被选择。在同一个”单选按钮组“中，所有单选按钮的 name 属性使用同一个值； 一个单选按钮组中是，同一时间只有一个单选按钮可以被选择。  |
| checkbox  | 复选框。必须使用 value 属性定义此控件被提交时的值。使用 checked 属性指示控件是否被选择。也可以使用 indeterminate 指示复选框在一种不确定状态（大多数平台上，显示为一条穿过复选框的水平线）。 |    
| file      | 此控件可以让用户选择文件。使用 accept 属性可以定义控件可以选择的文件类型。  |    
| hidden    | 不显示在页面上的控件，但它的值会被提交到服务器。  |
| image     | 图片提交按钮。必须使用 src 属性定义图片的来源及使用 alt 定义替代文本。还可以使用 height 和 width 属性以像素为单位定义图片的大小。  |    
| reset     | 用于将表单所内容设置为缺省值的按钮。   |
| submit    | 用于提交表单的按钮。  |    

> 代码示例：   
```
<body>
  <div>text：<input type="text"></div>
  <div>password：<input type="password"></div>
  <div>button：<input type="button" value="确定按钮"></div>
  <div>radio：<input type="radio" >1;<input type="radio" checked>2;</div>
  <div>checkbox:
    <input type="checkbox" value="one">one
    <input type="checkbox" value="two" checked>two
  </div>
  <div>file:<input type="file" accept=".docx"></div>
  <div>hidden:<input type="hidden"></div>
  <div>image:
    <input type="image" alt="图片" height="100px" width="100px"
    src="http://p1ibqa9uh.bkt.clouddn.com/17-12-26/59497439.jpg" > 
  </div>
  <br><br><br>
  <form action="/hello">
    <div>text：<input type="text"></div>
    <div><input type="reset" value="重置选项"></div>
    <div><input type="submit" value="提交"></div>
  </form>
</body>
```
> 在线测试网站：    

| [W3Cschool](http://www.w3school.com.cn/tiy/t.asp)  | [备用JS bin](http://js.jirengu.com/)  |  [备用JS BIN](http://jsbin.com/)  |      
| ---- | ---- | ----- |     
   


HTML5新增加的值：      

| 名字      | 作用           |
|----------:|:--------------|
| date      | 用于输入日期的控件（年，月，日，不包括时间）。 |
| datetime  | 基于 UTC 时区的日期时间输入控件（时，分，秒及几分之一秒）。***注：经测试Chrome、Safari、IE中这个属性没有控件出现。*** |
| datetime-local | 用于输入日期时间控件，不包含时区。  |
| time      | 用于输入不含时区的时间控件。   |   
| week      | 用于输入一个由星期-年组成的日期，日期不包括时区。 | 
| month     | 用于输入年月的控件，不带时区。 | 
| color     | 用于指定颜色的控件。  |
| email     | 用于编辑 e-mail 的字段。 合适的时候可以使用 :valid 和 :invalid CSS 伪类。 |    
| number    | 用于输入浮点数的控件。   |
| range     | 用于输入不精确值控件。如果未指定相应的属性，控件使用如下缺省值：`min：0`,`max：100`,`value：min + (max-min)/2，或当 max 小于 min 时使用 min`,`step：1`   |
| tel       | 用于输入电话号码的控件；换行会被自动从输入的值中移除A，但不会执行其他语法。可以使用属性，比如 pattern 和 maxlength 来约束控件输入的值。恰当的时候，可以应用 :valid 和 :invalid CSS 伪类。  |   
| url       | 用于编辑URL的字段。 The user may enter a blank or invalid address. 换行会被自动从输入值中移队。可以使用如：pattern 和 maxlength 样的属性来约束输入的值。 恰当的时候使可以应用 :valid 和 :invalid CSS 伪类。  |    
| search    | 用于输入搜索字符串的单行文本字段。换行会被从输入的值中自动移除。  |   

> 代码示例：   
```
<body>
  <div>日期date:<input type="date"></div>
  <div>日期时间：<input type="datetime"></div>
  <div>日期时间:<input type="datetime-local"></div>
  <div>时间：<input type="time"></div>
  <div>星期：<input type="week"></div>
  <div>月份month:<input type="month"></div>
  <div>颜色设置：<input type="color"></div>
  <div>email邮件:<input type="email"></div>
  <div>数字：<input type="number"></div>
  <div>范围：<input type="range" min="1" max="10" value="5"></div>
  <div>电话：<input type="tel"></div>
  <div>链接url:<input type="url"></div>
  <div>搜索：<input type="search"></div>
</body>
```

测试网站见上面。   










