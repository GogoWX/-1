# AJAX
> AJAX = 异步 JavaScript 和 XML。
AJAX 是一种用于创建快速动态网页的技术。
通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

### 创建XMLHttpRequest对象

```javascript
var xmlhttp;
if (window.XMLHttpRequest)
{
    //  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
	xmlhttp = new XMLHttpRequest();
}
else
{
    // IE6, IE5 浏览器执行代码
    xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
}
```
### 实例

```javascript
var xmlhttp;
function loadXMLDoc (url,cfunc) {
	if (window.XMLHttpRequest) {
    	// IE7+, Firefox, Chrome, Opera, Safari 代码
		xmlhttp=new XMLHttpRequest();
	}else{
    	// IE6, IE5 代码
		xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
	}
	xmlhttp.onreadystatechange=cfunc;
	xmlhttp.open("GET",url,true);
	xmlhttp.send();
}
function myFunction () {
	loadXMLDoc("/try/ajax/ajax_info.txt",function () {
		if (xmlhttp.readyState==4 && xmlhttp.status==200) {
			document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
		}
	});
}
```

### jQuery中的Ajax

```javascript
$(document).ready({
	$.ajax({
    	type: "GET",
        url: "url",
        dataType: "json",
        success: function (data) {
        	console.log("Ajax请求成功",data)
        }，
        error: function (jqXHR) {
        	alert("Ajax请求失败",request.status)
		}
	})
})
```

### 跨域的处理方法

> 一个域名地址的组成：
> http:// (协议) www(主域名). abc.com(子域名) : 8080(端口号) / script/jquery.js(请求资源地址)

1. 代理

