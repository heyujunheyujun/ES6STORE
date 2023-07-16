## 第七章：Set集合与Map集合

判断一个key在对象中是否存在，使用in运算符，注意：in运算符也会检索对象的原型，只有当对象原型为null时使用这个方法比较稳妥；<br>

### Set与WeakSet
Set类型是一种有序列表，含有一些相互独立的非重复值，通过Set集合可以快速访问其中的数据，更有效的追踪各种离散值；<br>
在Set集合中，不会对所有值及逆行强制的类型转换，数字5与字符串"5"都可以同时存在，不会被去重；<br>
set也可以用forEach方法进行遍历；<br>
注意：最好不要像访问数组元素那样直接通过索引访问集合中的元素，如有需要，最好先将Set集合转换成一个数组；<br>

Set与Weak Set的区别：<br>
1、最大的区别就是是否对初始对象进行强引用，导致垃圾回收机制无法回收；<br>
let set = new Set();<br>
let key = {};<br>
set.add(key);<br>
key = null;<br>
console.log(set.size); // 1<br>
key = [...set][0]; // 重新取回原始引用;<br>
可以看见，set集合保留了对key的引用；<br>
而在weak set中，集合只存储对象的弱引用，并且不可以存储原始值，集合中的弱引用如果是对象唯一的引用，则会被回收并释放相应的内存；<br>

2、Weak Set不接受原始值，如果数组中包含非对象值，程序抛出错误，Set接受原始值；<br>
let key1 = 1;<br>
let key2 = {};<br>
let key3 = {};<br>
new Set([key1, key2]); // ok<br>
new WeakSet([key1, key2]); // Uncaught TypeError: Invalid value used in weak set<br>
new WeakSet([key3, key2]); // ok<br>

3、Weak Set不可迭代，不能被用于for-of循环；<br>
4、Weak Set不暴露任何迭代器，不能使用keys()或values()方法；<br>
5、Weak Set不支持forEach方法；<br>
6、Weak Set不支持size属性；<br>

### Map(有序列表)与WeakMap(无序列表)
Map类型是一种储存着许多键值对的有序列表，其中的键名和对应的值支持所有的数据类型。<br>

WeakMap是弱引用Map集合，用于存储对象的弱引用，WeakMap集合中的键名必须是一个对象，如果使用非对象键名会报错；<br>
WeakMap集合最大的用途是保存Web页面中的DOM元素，当DOM元素消失时，可以自动销毁集合中的相关对象；<br>
WeakMap只支持两个操作键值对的方法，has和delete方法；<br>
