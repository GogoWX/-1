### 面向对象编程

> JavaScript 和java、C#的面向对象不同，JavaScript不区分类和实例的概念，而是通过原型（prototype）来实现面向对象编程。

##### 创建对象

当我们创建一个函数对象时：
```javascript
function boring() {
	return 'never mind'
}
```
它的原型链是：
> boring -> Function.prototype(函数的原型) ->Object.prototype -> null

由于Function.prototype定义了apply()等方法，因此，所有函数都可以调用apply()方法。

##### 构造函数

JavaScript还可以用一种构造函数的方法来创建对象。它的用法是，先定义一个构造函数：

```javascript
function Student(name) {
    this.name = name;
    this.hello = function() {
    	alert("Hello" + this.name + "!")
    }
}
```

用关键字new来调用这个函数，并返回一个对象：

```javascript
var xiaoming = new Student('小明');
xiaoming.name; // 小明
xiaoming.hello(); // Hello, 小明!
```

用new Student()创建的对象还从原型上获得了一个constructor属性，它指向函数Student本身：

```javascript
xiaoming.constructor === Student.prototype.constructor; // true
Student.prototype.constructor === Student; // true
Object.getPrototypeOf(xiaoming) === Student.prototype; // true
xiaoming instanceof Student; // true
```

如果我们通过new Student()创建了很多对象，这些对象的hello函数虽然名字和代码都相同，但却是不同的函数，实际上他们可以通过共享一个函数来减少内存，我们只要把hello函数移动到这些对象的共同原型对就可以了，也就是Student.prototype：

```javascript
function Student(name) {
    this.name = name;
}
Student.prototype.hello = function() {
    alert("Hello" + this.name + "!")
}
```

##### 原型继承

传统的基于Class的语言如Java、C++中，继承的本质就是扩展一个已有的Class，并生成一个新的SubClass。
JavaScript由于采用原型继承，所以无法直接扩展一个Class，我们需要把原型链修改为：

> new PrimaryStudent() -> PrimaryStudent.prototype -> student.prototype ->Object.prototype ->null

JavaScript的原型继承方法就是：

1. 定义新的构造函数，并在内部用call()调用希望“继承”的构造函数，并绑定this；

2. 借助中间函数F实现原型链继承，最好通过封装的inherits函数完成；

3. 继续在新的构造函数的原型上定义新方法。

把继承的动作用一个inherits()函数封装起来，可以重复使用，还可以隐藏函数F的定义：

```javascript
function inherits(Child,Parent) {
    var F = function() {};
    F.prototype = Parent.prototype;
    Child.prototype = new F();
    Child.prototype.constructor = Child;
}
//创建parent对象
function Student(props) {
    this.name = props || 'Unnamed'
}
Student.prototype.hello = function() {
    alert('Hello, ' + this.name + '!');
}
//创建child对象
function PrimaryStudent(props) {
    student.call(this,props);
    this.grade = props.grade || 1;
}
//实现原型链继承
inherits (PrimaryStudent,Student);
//绑定其他方法到PrimaryStudent原型上
PrimaryStudent.prototype.getGrade = function() {
    return this.grade;
}
```

##### class继承

> 新的关键字class从ES6开始正式被引入到JavaScript中。class的目的就是让定义类更简单。

用新的class关键字来编写Student，可以这样写：

```javascript
class student {
    constructor(name) {
    	this.name = name;
    }
    
    hello() {
    	alert('Hello, ' + this.name + '!');
    }
}
```

class的定义包含了构造函数constructor和定义在原型对象上的函数hello()（注意没有function关键字），这样就避免了Student.prototype.hello = function () {...}这样分散的代码。

class的继承，直接通过extends来实现：
```javascript
class PrimaryStudent extends Student {
    constructor(name,grade) {
    	super(name); //用super调用父类的构造方法
        this.grade = grade;
    }
    
    myGrade() {
    	alert('I am at grade ' + this.grade);
    }
}
```
