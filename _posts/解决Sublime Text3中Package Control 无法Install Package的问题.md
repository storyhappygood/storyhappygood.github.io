今天使用Sublime想要安装插件时发现点击Install Package提示报错
根据网上的解决方法发现问题的根源在于sublime进行插件下载时，sublime会调用channel_v3.json文件，
而这个文件的默认访问网址是这个
![](http://ww2.sinaimg.cn/large/006tNc79gy1g4680q56nlj30tw0i0gqc.jpg)
"channels":
	["https://packagecontrol.io/channel_v3.json"]
可在Preferences-> Package Settings->PackageControl->Settings-default中查看到，而这个网址无法访问
解决方法：
 打开Preferences-> Package Settings -> Package Control->Settings-user文件，在channels字段（如果没有channels字段可手动添加）中加入网址https://raw.githubusercontent.com/wilon/sublime/master/download/channel_v3.json

