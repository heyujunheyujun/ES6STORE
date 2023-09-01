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


1.typeof User === 'function'<br>
2.User类内部有[[isClassConstrctor]]，只能通过new关键字调用，如果不是的话会报错<br>
3.new User的时候就初始化了constructor构造器，constructor不是必须的，要对实例进行一些初始化操作时才写；<br>
4.每个new出来的User实例对象的constructor里面的属性都是唯一的，会给分配内存<br>
5.User类里面定义的方法是挂载到User.prototype原型里的，是所有实例对象共享<br>
6.User类的方法是不可枚举的，即不会被for..in遍历出来，而传统的构造函数的原型是可被枚举的。<br>
7.class类里面是自动启用严格模式的<br>
8.类的方法调用可能会有this丢失的问题，可以用箭头函数包裹一下做处理<br>
9.类的extends关键字就是继承，指向更深的原型<br>
10.super关键字相当于this.__proto__，在子类的方法中可以调用父类的方法，实现多态。也可在子类的constructor中super()继承父类的constructor属性。super不能调用箭头函数定义的方法<br>
11.static关键字是只有类本身才能访问，new出来的实例对象是无法访问的。是属于类自身的。<br>
12.子类可以继承父类的static的方法和属性，但同样是只有子类本身才能使用，实例对象无法访问。<br>
13.子类可以继承父类的protected的方法和属性<br>
14.private的方法和属性不能被继承，只能内部使用<br>
15.要实现子类继承多个类，可以使用Object,assign()方法合并<br>
