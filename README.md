# 前端模块化 #

声明：本文内容转载自我们群主大哥的文章[https://zhuanlan.zhihu.com/p/23554806?refer=icode](https://zhuanlan.zhihu.com/p/23554806?refer=icode)不过是我一字一字敲出来的哦！

## 一、CommonJS是什么，什么是模块化？AMD和CMD又是什么？ ##

1 模块化：指的就是遵守commonJS规范，解决不同js模块之间相互调用问题。

2 CommonJS：提供一个类似Python,Java标准库。应用CommonJS API编写程序，以实现使用JavaScript程序开发：

*服务器端JavaScript应用程序；*
	
*命令行工具；*
	
*图形界面应用程序；*
	
*混合应用程序。*

CommonJS是一种规范，而NodeJS是这种规范的实现。

过程如下：

A.js文件中调用另一个B.js文件，一定要在A.js中引入B.js

	require("B.js");

另一个被调用的js，也是就是B.js一定要对外提供接口。

	module.exports=B;
	
具体代码：

B.js

	javascript
	var b="hello";
	module.exports=b;//暴露一个接口，与b对接。这个接口既可以是函数，也可以是对象，甚至是数组。

A.js

	javascript
	var _b=require("/B.js");//实际过程中是B.js相对于A.js的路径；
	//此时——b获得了B.js的接口，这个接口指向B.js中的变量b。
	console.log(_b);//"hello";

## 二、模块化的一些工具 ##

1 gulp+browerify

2 webpack

3 requireJS

4 SeaJS

//为什么我没详细写，因为我不会 ^^;

## 三、模块化案例 ## 

1 前端mvc架构

·Vue组件化&模块化
·React组件化&模块化
·node.js每个文件都是模块

2 什么是MVC

·后端开发的一种概念

*即view(html+js+css+img)+controller(控制层)+model(数据模型)*

·前端演变了一套MVC体系：

·veiw(html+css+js)

*写静态页面css js img 及效果*

·controller（专注于实现服务和逻辑控制的层面叫做控制器）

*监听页面中请求和事件，处理请求和事件；向model请求数据，得到数据后绑定到页面*

·model(数据变量||ajax从服务端取回的数据)

*对外提供一些数据*


体现了一种分层的概念，让每个层面只做自己该做的行为，减少代码耦合和冗余

3 为什么使用MVC？

低耦合：

MVC将业务分为三层，减少了数据与业务的耦合性，增强了各层次功能的独立性，使得在需求改变时可能只需要改变其中一层就能完成服务。

复用性高：

三层业务功能分明，耦合度低，使各模块可以独立完成自身功能，降低了依赖性，具有很高的复用性。

利于批量生产和扩展：

复用性高使得在批量生产的时候可以根据需求进行模块的重用，加快了生产效率。并且模块化使得扩展也非常方便，模块只需根据规范进行编写，经审核后引入便可以实现扩展。

利于协作开发：

扩展性强使协作开发也变得非常方便，每个人根据自己的分工设计自己的模块，不与他人冲突，引入时也各行其职。

推广度及度高：

由于对协作开发的友好，使得MVC模式大受开发者的欢迎，使用这个模式的产品的推广及普及变得容易得多。


2016/11/23 16:47:32 










