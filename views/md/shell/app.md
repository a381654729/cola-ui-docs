# App对象

Cola Shell内置一个App对象，通过该对象可以完成一些跟App相关的操作。App中包含的方法有以下一些...

### prop(key, value)
基本参数设定，具体请参考 [基本参数设定](shell-setting) 。

### channel(config) 和 router(config)
配置频道和卡片，具体请参考 [频道和卡片](shell-router) 。

### open(path, config)
打开一个新的链接，此方法的基本用法与标准的window.open()有点像。
但是当我们要打开一个应用内的链接时，如果使用window.open()是会导致整个页面刷新的，而利用App.open()是不会导致整体刷新的，即实现的效果是应用内部的频道或卡片切换。

这里的config参数是一个可选参数，可以用于定义一些额外的选项，config通常是一个JSON对象，其中可以包含下列的子属性：
* replace	-	是否在浏览器的history中替换当前的路径，这样当用户点击浏览的回退按钮时浏览器将不会回退到当前的页面，而是回退到上一个页面。
* argument	-	传入到要打开的频道或卡片中的额外参数，注意此特性只对那些App内部的URL有效。
此参数可以在卡片页面中通过App.getArgument()方法来获得。
* callback	-	当开发的卡片被关闭是触发的回调方法。
该方法可以接收一个传入参数，是卡片页面向其父页面传回的返回值，该返回值应当在卡片页面中通过App.setReturnValue()方法来设置。
* target	-	相当于window.open()方法中的target参数。
如果target的值不是_self，那么此方法的执行效果将与window.open()完全一样，其他参数都将失效。

### getArgument(model)
获得父页面传入的参数，调用此方法时须传入当前当前卡片页面的model对象。

### setReturnValue(model, value)
设置当前卡片的返回值，调用此方法时须传入当前当前卡片页面的model对象。

### goLogin()
显示登录页。

此方法可以传入两种参数，它们的顺序不重要，Cola Shell会自动根据参数的类型来判断他们的作用。
* 如果参数为String类型，这表示登录成功之后将要自动打开的URL。如果不定义此参数则会再回到当前的页面。
* 如果参数类型为Function，这表示登录成功之后的回调方法。

### setTitle(model, title)
设置当前卡片的标题。

### boardcastMessage(message)
广播消息。

此处的message参数应该是一个JSON对象，其中包含两个子属性：
* type	-	消息类型，可以任意定义。
* data	-	消息的附带信息，可以任意定义。

假设我们调用下面的代码来广播一段消息...
`
App.boardcastMessage({
	type: "helloMessage",
	data: "Hey you guys."
});
`

我们可以在任何一个卡片的代码中利用下面的代码收听到这个消息...
`
$(window).on("helloMessage", function(data) {
	console.log(data); // 将打印Hey you guys.
});
`