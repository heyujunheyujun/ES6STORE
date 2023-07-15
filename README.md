# ES6STORE
深入理解ES6

第一章 块级作用域绑定


最佳实践：优先使用const，只在确实需要改变变量的值时才使用let；

var
1、通过var关键字声明的变量，都会被当成在当前作用域顶部声明的变量，就是提升机制；
2、无论是否声明var变量，直接在前面typeof取变量类型，都会被判断为undefind；
3、var设置为全局变量时，如果跟window的对象重复，则会修改window原本的对象，比如var RegExp = 0;那么原本的window.RegExp属性则修改为0；

let
1、用let关键字声明的变量，都可以限制在当前代码块{}中，let变量不会被提升；
2、如果在let声明之前用typeof取变量类型，则会报语法错误（临时死区）；但如果没有用let声明，直接用typeof判断则输出undefind；
3、let设置为全局变量时，如果跟window的对象重复，会遮蔽掉原本的对象，但不会破坏window原本的属性；

const
1、const声明必须设置初始化，且不能修改，绑定的是引用关系，不能修改绑定，但允许修改绑定的值，比如数组和对象的值都可以修改。

第二章
indexOf()与includes()的异同
同：
  两个方法都接收两个参数，第一个参数必传，第二个参数可选，为开始搜索的位置；
不同：
  indexOf的返回值为搜索结果的索引值，若未搜索到则返回-1；includes返回布尔值；
  indexOf传入的第一个参数可接收字符串或正则表达式，而includes只能接收字符串；

