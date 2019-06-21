#JavaScript学习

##基本语法

###常量和变量

+ 常量
    + 整形常量：可以使用十六进制，十进制或者八进制来表示
    + 实型常量：9.8 5E7
    + 布尔值：true false
    + 字符型常量：单引号或者双引号括起来的一个或几个字符
    + 空值：null
    + 特殊字符：以反斜杠/开头的不可显示的字符
+ 变量
    + 变量名：字母数字下划线，避开关键字，联系意义
    + 变量定义：var city1;
    + 变量赋值：
        + var city1=100;
        + var city2=北京;
        + var city3=true;
        + var city4=null;
    + 变量分为局部变量和全局变量
    
### 表达式和运算符

+ 表达式
    + 常量，变量，布尔和运算符的集合
+ 运算符
    + 算术运算符
    + 比较运算符
    + 逻辑运算符

### 基本运算

+ if else语句
    + if(条件)<br>
      {执行语句1}<br>
      else<br>
      {执行语句2}
+ for语句
    + for(初始化;条件;增量)<br>
      {语句集}
+ switch语句
    + switch()<br>
    {<br>case 条件1:语句块1<br>
     case 条件2:语句块2<br>
     default: 语句块3<br>
    }
+ while语句
    + while(条件)<br>
    {语句集}
+ break语句
    + break;
+ continue语句
    + continue；
    
##事件

+ 所谓事件，就是鼠标或者键盘的动作
+ 由鼠标或者键盘引发的一连串的动作，称之为事件驱动
+ 对事件进行处理的程序或者函数，称之为事件处理程序

###onclick事件
+ 鼠标单击事件
```
<script>
    function displayDate()
    {
        document.getElementById("demo").innerHTML=Date();
    }
</script>
<p id="demo">This is a paragraph.</p>
<button type="button" onclick="displayDate()">Display Date</button>
```
###onchange事件
+ 与表单相关的事件,当利用text或testarea元素输入的字符值发生改变时发生该事件，同时当在select表格中的一个状态选项发生改变时也会引发该事件

```
<textarea name="textarea" cols="50" rows="5" onchange=alert("输入留言内容")></textarea>
```
```
<input type="text" onchange=alert("输入留言内容")>
```
```
<select>
  <option value="volvo">Volvo</option>
  <option value="saab">Saab</option>
  <option value="opel">Opel</option>
  <option value="audi">Audi</option>
</select>
```
###onselect事件
+ onSelect事件是当文本框中的内容被选中时所发生的事件
```
<input value="请输入所选择的内容" onselect=alert("选择输入的名称")>
```
###onfocus事件
+ 当单击表单对象时，即将光标放在文本框或选择框上时产生onfocus事件。
```
<input type="text" value="音乐" onfocus=alert("选择音乐！")>音乐
```
###onload事件
加载网页文档时，会产生该事件。onload事件的作用是在首次载入一个页面文件时检测cookie的值，并用一个变量为其赋值，使其可以被源代码使用。
````
<head>
	<script>
		function MM_popuMsg(msg) {
			alert(msg)
		}
	</script>
</head>
<body onload="MM_popuMsg('欢迎光临')">
````
###onunload事件
当退出网页时引发onunload事件，并可更新cookie的状态。
````
<body onload="MM_popuMsg('欢迎光临')" onunload="MM_popuMsg('关闭本文档')">、
````
###onblur事件
失去焦点onblur事件正好与获得焦点事件相对，当text对象，textarea对象或者select对象不再拥有焦点而推到后台时，引发该事件。
```
<br>账号<input type="text" onblur=alert("文档中的'账号'文本域失去焦点") />
```
###onmouseover事件
onmouseover是当鼠标指针移动到某对象范围的上方时触发的事件。
###onmouseout事件
onmouseout是当鼠标指针离开某对象范围时触发的事件。
```
<script>
    function bigImg(x){
        x.style.height="64px";
        x.style.width="64px";
    }
    function normalImg(x){
        x.style.height="32px";
        x.style.width="32px";
    }
</script>
<img onmouseover="bigImg(this)" onmouseout="normalImg(this)" border="0" src="smiley.gif" alt="Smiley" width="32" height="32">
```
###ondblclick事件
鼠标双击时触发事件
```
<p ondblclick=alert("双击了")>双击这段触发一个事件</p>
```
##浏览器的内部对象
+ 浏览器对象（navigator）：提供有关浏览器的信息。
+ 文档对象（document）：document对象包含了与文档元素一起工作的对象。
+ 窗口对象（windows）：windows对象处于对象层次的最顶端，它提供了处理浏览器窗口的方法和属性。
+ 位置对象（location）：location对象提供了与当前打开的URL一起工作的方法和属性，它是一个静态的对象。
+ 历史对象（history）：history对象提供了与历史清单有关的信息。

###navigator对象
navigator对象可以用来存取浏览器的相关信息
```
<script>
    document.write(navigator.appName+"<br>");//浏览器的名称
	document.write(navigator.appVersion+"<br>");//浏览器的版本
	document.write(navigator.appCodeName+"<br>");//浏览器的代码名称
	document.write(navigator.plugins+"<br>");//可以使用的插件信息
	document.write(navigator.platform+"<br>");//浏览器所使用的平台，如win32等
	document.write(navigator.cookieEnabled);//浏览器的cookie功能是否打开
</script>
```
###document对象
document对象中主要有三个重要的对象：
+ anchor锚对象：是指<a name=...></a>标记在HTML源代码中存在时产生的对象，它包含着文档中所有的anchor信息。
+ links链接对象：是指用<a href=...></a>标记链接一个超文本或者超媒体的元素作为一个特定的URL。
+ form窗体对象：是文档对象的元素，它含有多种格式的对象存储信息，使用它可以在JavaScript脚本中编写程序，并可以用来动态的改变文档的行为。

document对象有以下方法：
+ 输出显示write（）和writeln（）：该方法主要用来实现在web页面上的输出信息。
```
<script>
    function Links()
    {
        n=document.links.length;//获得连接个数
        s='';
        for(j=0;j<n;j++)
            s=s+document.links[j].href+"\n";//获得链接地址
        if (s=="")
            s="没有任何链接"
        else
            alert(s);
    }
</script>

<input type="button" value="所有链接地址" onclick="Links()"><br>
<p>
    <a href="https:www.baidu.com">文档1</a>
    <a href="https:www.baidu.com">文档2</a>
    <a href="https:www.baidu.com">文档3</a>
</p>
```
##windows对象
windows对象处于对象层次的最顶端，它提供了处理navigator窗口的方法个属性。JavaScript的输入可以通过windows对象来实现。

windows对象常用的方法：

| 方法 | 方法的含义及参数说明 |
|:----:|:----:|
| open(url,windowName,parameterlist) | 创建一个新窗口，三个参数分别用于设置URL地址，窗口名称和窗口打开的属性（一般可以包括宽度，高度，定位，工具栏等）|
| close() | 关闭一个窗口 |
| alert(text) | 弹出式窗口，text参数为窗口中显示的文字 |
| promt(text,defaulttext) | 弹出提示框，text为窗口中的文字，defaulttext参数用来设置默认情况下显示的文字 |
| moveBy(水平位移，垂直位移) | 将窗口移至指定的位移 |
| moveTo（x,y）| 将窗口移动到指定的坐标 |
| resizeTo(水平位移，垂直位移) | 将给定的位移量重新设置窗口大小 |
| back() | 页面后退 |
| forward() | 页面前进 |
| home | 返回主页 |
| stop | 停止装载页面 |
| print() | 打印网页 |
| status |状态栏信息 |
| location | 当前窗口的URL信息 |

```
<script>
    function myfunc() {
        window.open("https://www.baidu.com", '', width =600,height=300);
    }
</script>
<input type="button" value="百度一下" onclick="myfunc()"><br>
```

##location对象
location对象是一个静态的对象，它描述的是某一个窗口对象所打开的地址。
###常用的location属性
| 属性 | 实现的功能 |
|:----:|:----:|
| protocal | 返回地址的协议，取值为http：，https：file：等 |
| hostname | 返回地址的主机名，例如http:www.baidu.com/china/ 地址的主机名为www.baidu.com |
| port | 返回地址的端口号，一般http的端口号是80 |
| host | 返回主机名和端口号，如www.com:8080 |
| pathname | 返回路径名，如http://a.com/d/index.html |
| hash | 返回"#"以及其后的内容，如地址为c.html#chapter4，则返回#chapter4；如果地址里没有"#"，则返回空字符串 |
| search | 返回"？"以及其后的内容，如果地址里没有"？"，则返回空字符串 |
| href | 返回整个地址，即返回浏览器的地址栏中显示的内容 |
###loacation对象常用的方法
+ reload():相当于IE浏览器上的"刷新"功能
+ repalce():打开一个URL，并取代历史对象中当前位置的地址。用这个方法打开一个URL后，单击浏览器的"后退"按钮将不能返回到之前的页面。
##history对象
history'对象是浏览器的浏览历史，以下为history对象常用的方法。
+ back（）：后退，与单击"后退"按钮是等效的。
+ forward ：前进，与单击"前进按钮"是等效的。
+ go():该方法用来进入指定的页面。
```
<input type="button" onclick="history.back()" value="返回">
<input type="button" onclick="history.forward()" value="前进">
```
