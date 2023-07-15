## 第四章：拓展对象的功能性

Object.is(arg1, arg2)方法来弥补全等运算符的不准确运算；多数情况下与===运算符相同，唯一区别是+0和-0被识别为不相等并且NaN与NaN等价；<br>
Object.assign()方法接受一个接收对象和任意数量的源对象，最终返回接收对象。同名属性后面的会覆盖前面的。<br>

改变对象的原型<br>
Object.getPrototypeOf()方法返回指定对象的原型；<br>
Object.setPrototypeOf()方法来改变指定对象的原型，接收两个参数：被改变原型的对象及替换第一个参数原型的对象；<br>
对象原型的真实值被存储在内部专用属性[[Prototype]]中，调用Object.getPrototypeOf()方法返回储存在其中的值，调用Object.setPrototypeOf()方法改变其中的值。<br>

简化原型访问的Super引用<br>
es6引入了Super引用的特性，使用它可以更便捷地访问对象原型；Super引用相当于指向对象原型的指针；<br>

### 正式的方法定义
es6定义的方法：在对象内定义方法，它有一个内部的[[HomeObject]]属性来容纳这个方法从属的对象。<br>
let person = {<br>
  getGreeting(){<br>
    return 'Hello';<br>
  }<br>
}<br>
getGreeting方法的[[HomeObject]]属性值为person，当使用Super引用时很重要；<br>
Super的所有引用都是通过[[HomeObject]]属性来确定后续的运行过程。第一步是在[[HomeObject]]属性上调用Object.getPrototypeOf()方法来检索原型的引用；然后搜寻原型找到同名的函数，最后，设置this绑定并且调用相应的方法。<br>
