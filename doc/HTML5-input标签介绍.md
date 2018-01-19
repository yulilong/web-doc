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
        <th width="130px">属性</th> <th>值</th> <th>描述</th>
    </tr>
    <tr>
        <td>type </td>
        <td>
          text  <br>password  <br>button  <br>radio   <br>
          checkbox   <br>file   <br>hidden   <br>
          image   <br>reset   <br>submit   <br>
          date <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px">  <br>
          datetime <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px">  <br>
          datetime-local <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"> <br>
          time  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px">  <br>
          week  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px">  <br>
          month <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px">   <br>
          color <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px">   <br>
          email  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px">  <br>
          number <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px">   <br>
          range  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px">  <br>
          tel <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"><br>
          url <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"><br>
          search <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"><br>
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
        3. `video/*`视频文件 <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"> <br>
        4. `image/*`图片文件 <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"> <br>
      </td>
      <td>如果该元素的 type 属性的值是file,则该属性表明了服务器端可接受的文件类型；否则它将被忽略。该属性的值必须为一个逗号分割的列表,包含了多个唯一的内容类型声明</td>
    </tr>
    <tr>
      <td>autocomplete <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"> </td>
      <td> on: 自动填充值 <br> off: 用户必须手动填值 <br> </td>
      <td>这个属性表示这个控件的值是否可被浏览器自动填充。如果type属性的值是hidden、checkbox、radio、file，或为按钮类型（button、submit、reset、image），则本属性被忽略。</td>
    </tr>
    <tr>
      <td>autofocus <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>autofocus</td>
      <td>在页面加载时具有焦点（自动获得焦点），除非用户将其覆盖，例如通过键入不同的控件。文档中只有一个表单元素可以具有autofocus属性，它是一个布尔值。 如果type属性设置为隐藏则不能应用</td>
    </tr>
    <tr>
      <td>checked</td> <td>checked</td>
      <td>该属性表示该控件为默认选中状态，如果input标签type属性值为radio或checkbox才有效，其他无效。</td>
    </tr>
    <tr>
      <td>disabled </td> <td>disabled </td>
      <td>这个布尔属性表示此表单控件不可用。并且，禁用的控件的值在提交表单时也不会被提交。如果 type 属性为  hidden，此属性将被忽略。</td>
    </tr>
    <tr>
      <td>form <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>同一文档中&lt;form&gt;元素的id</td>
      <td>如果未指定此属性，则此&lt;input&gt;元素必须是&lt;form&gt;元素的后代。 该属性使您可以将&lt;input&gt;元素放置在文档中的任何位置，而不仅仅是作为其表单元素的后代。</td>
    </tr>
    <tr>
      <td>formaction <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>URL</td>
      <td>覆盖表单的 action 属性。只有 type="submit" 以及 type="image"才有效。</td>
    </tr>
    <tr>
      <td>formenctype <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>
        application/x-www-form-urlencoded ：在发送前对所有字符进行编码（默认）。 <br>
        multipart/form-data : 不对字符编码。当使用有文件上传控件的表单时，该值是必需的。 <br>
        text/plain: 将空格转换为 "+" 符号，但不编码特殊字符。 <br>
      </td>
      <td>覆盖表单的 enctype 属性。只有 type="submit" 以及 type="image"才有效。</td>
    </tr>
    <tr>
      <td>formmethod <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>get <br> post <br></td>
      <td>覆盖表单的 method 属性。只有 type="submit" 以及 type="image"才有效。</td>
    </tr>
    <tr>
      <td>formnovalidate <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>novalidate</td>
      <td>覆盖表单的 novalidate 属性。如果使用该属性，则提交表单时不进行验证。</td>
    </tr>
    <tr>
      <td>formtarget <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>
        _blank :在新窗口中将表单提交到文档。 <br> _self: 在同一框架中将表单提交到文档。（默认）<br>
        _parent: 在父框架中将表单提交到文档。<br> _top: 在整个窗口中将表单提交到文档。
      </td>
      <td>覆盖表单的 target 属性。只有 type="submit" 以及 type="image"才有效。</td>
    </tr>
    <tr>
      <td>height  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>长度单位</td>
      <td>定义 input 字段的高度。（适用于 type="image"）</td>
    </tr>
    <tr>
      <td>width <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>长度单位</td>
      <td>定义 input 字段的宽度 。（适用于 type="image"）</td>
    </tr>
    <tr>
      <td>list  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>datalist-id</td>
      <td>引用包含输入字段的预定义选项的 datalist 。</td>
    </tr>
    <tr>
      <td>max  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>number <br> date</td>
      <td>规定输入字段的最大值。请与 "min" 属性配合使用，来创建合法值的范围。</td>
    </tr>
    <tr>
      <td>maxlength </td> <td>number </td> <td>规定输入字段中的字符的最大长度。</td>
    </tr>
    <tr>
      <td>max  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>number <br> date</td>
      <td>规定输入字段的最小值。请与 "max" 属性配合使用，来创建合法值的范围。</td>
    </tr>
    <tr>
      <td>multiple  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td> </td>
      <td>该属性指示用户能否输入多个值。这个属性仅在type属性为email或file的时候生效 ; 否则被忽视.</td>
    </tr>
    <tr>
      <td>name </td> <td>field_name </td> <td>定义 input 元素的名称。与表单数据一起提交。</td>
    </tr>
    <tr>
      <td>pattern  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>正则表达式 </td>
      <td>检查控件值的正则表达式.。pattern必须匹配整个值，而不仅仅是某些子集。当类型属性的值为text, search, tel, url 或 email时，此属性适用，否则将被忽略。</td>
    </tr>
    <tr>
      <td>placeholder  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>text文本 </td>
      <td>提示用户输入框的作用。用于提示的占位符文本不能包含回车或换行。仅适用于当type 属性为text, search, tel, url or email时; 否则会被忽略。</td>
    </tr>
    <tr>
      <td>readonly </td>
      <td>readonly </td>
      <td>规定输入字段为只读。如果控件的 type 属性为hidden, range, color, checkbox, radio, file 或 type时，此属性会被忽略。</td>
    </tr>
    <tr>
      <td>required</td>
      <td>required</td>
      <td>这个属性指定用户在提交表单之前必须为该元素填充值. 当type属性是hidden,image或者按钮类型(submit,reset,button)时不可使用. :optional 和 :required CSS 伪元素的样式将可以被该字段应用作外观.</td>
    </tr>
    <tr>
      <td>size</td> <td></td>
      <td>控件的初始大小。以像素为单位。但当type  属性为text 或 password时, 它表示输入的字符的长度。从HTML5开始, 此属性仅适用于当 type 属性为 text, search, tel, url, email,或 password；否则会被忽略。 此外，它的值必须大于0。 如果未指定大小，则使用默认值20。 </td>
    </tr>
    <tr>
      <td>src</td> <td>URL</td>
      <td>如果type属性的值是image, 这个属性指定了按钮图片的路径; 否则它被忽视.</td>
    </tr>
    <tr>
      <td>step  <img src="https://yulilong.github.io/web-doc/img/HTML5-icon.jpg" height="15px"></td>
      <td>number </td>
      <td>使用min和max 属性来限制可以设置数字或日期时间值的增量。它可以是任意字符串或是正浮点数。如果此属性未设置，则控件仅接受大于最小步长值的倍数的值。</td>
    </tr>
    <tr>
      <td>value</td> <td>URL</td>
      <td>控件的初始值. type 属性是radio或checkbox时value必填，其他的是可选的。</td>
    </tr>
  </table>


### type属性中值的介绍   

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

### type属性值的兼容性   

| 值      | IE    | Edge     | Firefox | Chrome | Safari | Opera | 
|------:|:------|:-----|:-----|:-----|:-----|:-----|
| [date, time, datetime-local, month & week](https://caniuse.com/#search=date) | 不支持（6~11） | 13以上 | 57以上部分支持 | 25以上 | 不支持 | 10.1以上 | 
| [color](https://caniuse.com/#search=color%20input) | 不支持（6~11）| 14以上 | 29以上 | 20以上 | 11以上 | 17以上 |  
| [Email, telephone & URL](https://caniuse.com/#search=Email,%20telephone%20%26%20URL) | 10以上 | 12以上 | 4以上 | 5以上 | 5以上 | 10.1以上 |    













### 其他信息   

|       |      |
|------:|:------|
|百度统计浏览器市场份额 |  http://tongji.baidu.com/data/browser    
| Opera 浏览器 | http://www.opera.com/zh-cn  、   http://www.oupeng.com/     |
| Firefox 浏览器 | http://www.firefox.com.cn/   
| Chrome 浏览器（需科学上网）  | https://www.google.cn/chrome/browser/desktop/index.html    







