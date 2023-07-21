## 第九章：Javascript中的类

基本的类声明语法：<br>
class Person {<br>
  constructor(name) {<br>
    this.name = name;<br>
  }<br>
  sayName() {<br>
    console.log(this.name);<br>
  }<br>
}<br>
类与自定义类型之间的差异：<br>
1、函数声明可以被提升，而类声明与let声明类似，不能被提升；真正执行声明语句之前，它们会一直存在于临时死区中。<br>
2、类声明中的所有代码自动运行在严格模式下，而且无法强行让代码脱离严格模式执行。<br>
3、在自定义类型中，需要通过Object.defineProperty()方法手动指定某个方法为不可枚举；而在类中，所有方法都是不可枚举的。<br>
4、每个类都有一个名为[[Construct]]的内部方法，通过关键字new调用那些不含[[Construct]]的方法会导致程序抛出错误。<br>
5、使用除关键字new以外的方式调用类的构造函数会导致程序抛出错误。<br>
6、在类中修改类型会导致程序报错。<br>

通过立即调用类构造函数可以创建单例。用new调用类表达式，紧接着通过一对小括号调用这个表达式。<br>
let person = new class {<br>
  constructor(name) {<br>
    this.name = name;<br>
  }<br>
  sayName() {<br>
    console.log(this.name);<br>
  }<br>
}('Nicholas');<br>

person.sayName(); // Nicholas<br>

静态成员 static<br>
不可在实例中访问静态成员，必须要直接i在类中访问静态成员。<br>

继承与派生类<br>
继承自其他类的类被称为派生类，如果在派生类中指定了构造函数则必须要调用super()，如果不这样做程序会报错。如果选择不使用构造函数，则当创建新的类实例时会自动调用super()并传入所有参数。<br>
class Square extends Rectangle {<br>
  // 没有构造函数<br>
}
class Square extends Rectangle {<br>
  constructor(...args) {<br>
    super(...args);<br>
  }<br>
}<br>

使用super()的小提示：<br>
1、只可在派生类的构造函数中使用super()，如果尝试在非派生类（不是用extends声明的类）或函数中使用则会导致程序抛出错误。<br>
2、在构造函数中访问this之前一定要调用super()，它负责初始化this，如果在调用super()之前尝试访问this会导致程序出错。<br>
3、如果不想调用super()，则唯一的方法是让类的构造函数返回一个对象。<br>

类方法遮蔽：<br>
派生类中的方法会覆盖基类中的同名方法。<br>
静态成员继承：<br>
如果基类有静态成员，那么这些静态成员在派生类中也可以用。<br>

new.target<br>
在类的构造函数中使用new.target来确定类是如何被调用的，new.target等于类的构造函数。<br>
class Rectangle {<br>
  constructor(length) {<br>
    console.log(new.target === Rectangle);<br>
    this.length = length;<br>
  }<br>
}<br>
let obj = new Rectangle(3); //true<br>
注意：派生类调用基类的构造函数，new.target指向的是当前派生类。<br>

因为类必须通过new关键字才能调用，所以在类的构造函数中，new.target属性永远不会是undefined；<br>