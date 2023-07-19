## 第八章：迭代器和生成器

什么是迭代器？<br>
迭代器是一种特殊对象，它具有一些专门为迭代过程设计的专有接口，所有的迭代器对象都有一个next方法，每次调用都返回一个结果对象。结果对象有两个属性；一个是value，表示下一个将要返回的值；另一个是done，它是一个布尔类型的值，当没有更多可返回数据时返回true。迭代器还会保存一个内部指针，用来指向当前集合中值的位置，每次调用next方法，都会返回下一个可用的值。<br>

什么是生成器？<br>
生成器是一种返回迭代器的函数，通过function关键字后的星号（*）来表示，函数中会用到新的关键字yield。<br>
function *createIterator() {<br>
  yield 1;<br>
  yield 2;<br>
  yield 3;<br>
}<br>
let iterator = createIterator();<br>
console.log(iterator.next().value); // 1<br>
console.log(iterator.next().value); // 2<br>
console.log(iterator.next().value); // 3<br>

或者表达式写法：<br>
let createIterator = function *(items) {}<br>
yield关键字可以通过它来指定调用迭代器的next()方法时的返回值及返回顺序。<br>
生成器函数每当执行完一条yield语句后函数就会自动停止执行。直到再次调用它的next方法才会继续执行yield语句。<br>
yield关键字只可在生成器内部使用，且必须在该函数作用域下，不能是生成器的子作用域，即不能穿透函数边界。<br>
注意：不能用箭头函数来创建生成器；<br>

可迭代对象和for-of循环<br>
可迭代对象具有Symbol.iterator属性，是一种与迭代器密切相关的对象。Symbol.iterator通过指定的函数可以返回一个作用于附属对象的迭代器。所有的集合对象（数组、Set集合及Map集合）和字符串都是可迭代对象，这些对象中都有默认的迭代器。<br>
注意：生成器默认会为Symbol.iterator属性赋值，所以通过生成器创建的迭代器都是可迭代对象；<br>
for-of循环每执行一次都会调用可迭代对象的next方法，并将迭代器返回的结果对象的value属性存储在一个变量中，循环将持续执行这一过程直到返回对象的done属性的值为true。<br>

访问默认迭代器<br>
可以通过Symbol.iterator来访问对象默认的迭代器。<br>
let values = [1,2,3];<br>
let iterator = values[Symbol.iterator]();<br>
console.log(iterator.next()); // "{value: 1, done: false}"<br>
console.log(iterator.next()); // "{value: 2, done: false}"<br>
console.log(iterator.next()); // "{value: 3, done: false}"<br>
console.log(iterator.next()); // "{value: undefined, done: true}"<br>

使用typeof object[Symbol.iterator] === 'function'来检测是否是可迭代对象；<br>

内建迭代器<br>
数组、Map集合与Set集合都内建了三种迭代器：<br>
entries()返回多个键值对；<br>
values()返回集合的值；<br>
keys()返回集合中所有键名；<br>
不同集合类型的默认迭代器不同，数组和Set集合的默认迭代器是values方法，Map集合的默认迭代器是entries方法。<br>
WeakMap集合与WeakSet集合没有内奸的迭代器，由于要管理弱引用，因而无法确切地直到集合中存在的值，也就无法迭代这些集合了。<br>

字符串迭代器<br>
es5之后，字符串慢慢变得更像数组了，可以通过for-of遍历字符串。<br>

NodeList迭代器<br>
NodeList类型代表页面文档中所有元素的集合，可以用for-of来进行迭代。<br>

生成器可以通过return指定返回值，并提前退出函数执行，后面的代码不会被执行；<br>