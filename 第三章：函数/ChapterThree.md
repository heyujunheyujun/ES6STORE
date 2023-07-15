## 第三章：函数

默认参数的临时死区<br>
1、定义参数时会为每个参数创建一个新的标识符绑定，该绑定在初始化之前不可被引用，如果试图访问会导致程序抛出错误，所以后面的参数可以引用前面的参数，而前面的参数不能引用后面定义的参数，这就是临时死区；<br>
2、函数参数有自己的作用域和临时死区，其与函数体的作用域是各自独立的；<br>

js函数有两个不同的内部方法：[[Call]]和[[Construct]]<br>
1、当通过new关键字调用函数时，执行的是[[Construct]]函数，它负责创建一个通常被称作实例的新对象，然后再执行函数体，将this绑定到实例上；<br>
2、如果直接调用函数，则执行[[Call]]函数，从而直接执行代码中的函数体。具有[[Construct]]方法的函数被统称为构造函数；<br>
3、不是所有的函数都有[[Construct]]方法，因此不是所有函数都可以通过new调用，例如箭头函数就没有[[Construct]]；<br>

### es5 -> 通过instanceof判断函数被new调用的方法
由于[[Construct]]方法会创建一个新实例，并将this绑定到新实例上；（无法区分是通过call/apply还是new调用得到的实例）<br>
function Person(name) {<br>
  if (this instanceof Person) {<br>
    this.name = name;<br>
  } else {<br>
    throw new Error('必须通过new关键字调用');<br>
  }<br>
}<br>

let person = new Person('nora');<br>
let notAPerson = Person('nora'); // 抛出错误<br>
let callPerson = Person.call(person, 'nora'); // 有效，无法区分是通过call/apply还是new调用得到的实例<br>

### es6 -> 通过元属性new.target
当调用函数的[[Construct]]方法时，new.target被赋值为new操作符的目标，通常是新创建对象实例，也就是函数体内this的构造函数；如果调用[[Call]]方法，则new.target的值为undefined；<br>
function Person(name) {<br>
  if (typeof new.target !== 'undefined') {<br>
    this.name = name;<br>
  } else {<br>
    throw new Error('必须通过new关键字调用');<br>
  }<br>
}<br>

let person = new Person('nora');<br>
let callPerson = Person.call(person, 'nora'); // 抛出错误<br>

### 箭头函数
与传统函数的不同有以下几个方面：<br>
1、没有this/super/arguments/new.target绑定<br>
箭头函数中的this、super、arguments、new.target这些值由外围最近一层非箭头函数决定；<br>
2、不能通过new关键字调用<br>
3、没有原型<br>
4、不可以改变this的绑定<br>
5、不支持arguments对象，调用的都是上一层函数的arguments对象<br>
6、不支持重复的命名参数<br>