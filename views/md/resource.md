# 国际化

Cola中提供了一个cola.resource()方法用于完成国际化资源的初始化和调用。

### 初始化国际化资源
如果我们为cola.resource()方法传入的参数是一个JSON对象，那么Cola将会利用这个JSON初始化一组国际化资源。例如：
```
cola.resource({
	"ok": "OK",
	"cancel": "Cancel",
	"reset": "Reset",
	"email": "Email",
	"password": "Password"
});
```

### 引用国际化资源
引用一个国际化资源时，我们需要向cola.resource()传入要引用的资源的key。例如：
```
console.log(cola.resource("ok")); // 根据之前初始化的结果，此代码的输出为"OK"
```

### 带有参数的国际化资源
国际化资源可以带有参数，例如：
```
cola.resource({
	"welcomeMessage": "{0}你好！欢迎进入{1}的世界！"
});
```
在使用时我们可以这样来调用...
```
cola.resource("welcomeMessage", "Nick", "Cola-UI"); // 我们得到的消息将是“Nick你好！欢迎进入Cola-UI的世界！”
```

### 利用表达式引用国际化资源
Cola的表达式中默认已支持了一个名为resource()的隐式方法，可供我们引用国际化资源。例如我们可以在HTML中这样写：
```
<span c-bind="resource('welcomeMessage', 'Nick', 'Cola-UI')"></span>
```

由于引用的国际化资源通常在一个页面的生命周期内是不会改变的。因此，我们可以将上面的写法微调成下面这种，以改善表达式的执行效率：
```
<span c-bind="=resource('welcomeMessage', 'Nick', 'Cola-UI')"></span>
```

### 国际化资源的管理
在实际的使用过程中，建议把每一个语种的国际化资源保存在一个独立的文件中。这样，只要根据实际需要装载特定的资源文件就可以实现前端的国际化了。
在为每一个语种的资源文件命名时，建议参考 http://tools.ietf.org/html/bcp47 的规范，但这不是必须的。

### 国际化Cola中自带的资源字串
TODO...