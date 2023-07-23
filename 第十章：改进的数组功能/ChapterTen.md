## 第十章：改进的数组功能

### 创建数组
ES6新增了Array.of()和Array.from()两个方法；<br>
Array.of是用来规避通过Array构造函数创建数组时的怪异行为；<br>
let items = new Array(2);<br>
console.log(items.length); // 2<br>
console.log(items[0]); // undefined<br>
console.log(items[1]); // undefined<br>

items = new Array('2');<br>
console.log(items.length); // 1<br>
console.log(items[0]); // '2'<br>
从上面可以看到，传入数值型参数和字符串类型的参数的表现不一致，显得很怪异，而Array.of方法就是解决这个怪异问题。<br>

Array.of总会创建一个包含所有参数的数组<br>
let items = Array.of(2);<br>
console.log(items.length); // 1<br>
console.log(items[0]); // 2<br>

Array.from方法接受可迭代对象或类数组对象作为第一个参数，最终返回一个数组。第二个参数接受一个回调函数，用来处理每一个遍历的元素，第三个参数表示映射函数的this值指向，从而无需通过调用bind方法来指定this值了。<br>
Array.from(arr, function(){}, this指向的对象);<br>

### 为所有数组添加的新方法
find()和findIndex()<br>
find()和findIndex()都接受两个参数，一个是回调函数，一个是可选参数用于指定回调函数中的this值。二者唯一的区别就是find返回查找到的第一个值，findIndex返回查找到的值的索引。<br>

fill()<br>
fill()方法可以用指定的值填充一至多个数组元素；<br>
items.fill(0,1,3); 表示对items数组的索引为1的位置，结束索引为3（不包括3）的位置填充0；<br>

copyWithIn()<br>
copyWithIn()方法从数组中复制元素的值，需要传入两个参数，一个是该方法开始填充值的索引位置，一个是开始复制值的索引位置；第三个可选参数为不包含结束索引，用于指定停止复制值的位置。<br>

### 定型数组
数组缓冲区是所有定型数组的根基，它是一段包含特定数量字节的内存地址，可以通过ArrayBuffer构造函数来创建数组缓冲区。可以通过byteLength属性查看缓冲区的字节数量；也可以通过slice()方法分割已有数组缓冲区来创建一个新的（就是切片的概念）。<br>
tips：数组缓冲区包含的实际字节数量在创建时就已确定，可以修改缓冲区内的数据，但是不能改变缓冲区的尺寸大小；<br>

通过视图操作数组缓冲区<br>
数组缓冲区时内存中的一段地址，视图是用来操作内存的接口，可以读取和写入数据。DataView类型是一种通用的数组缓冲区视图，其支持所有8种数值型数据类型。<br>
要使用DataView，首先要创建一个ArrayBuffer实例，然后用这个实例来创建新的DataView<br>
let buffer = new ArrayBuffer(10);<br>
let view = new DataView(buffer); // 默认的包含所有<br>
let view2 = new DataView(buffer, 5, 2); // 包含位于索引5和6的字节<br>
由此可以看出，可以基于同一个数组缓冲区创建多个view<br>

获取视图的信息<br>
可以通过以下几种只读属性来获取视图的信息<br>
buffer：视图绑定的数组缓冲区<br>
byteOffset：偏移量，获取缓冲区的开始索引位置<br>
byteLength：默认是缓冲区的长度<br>

读取和写入数据<br>
...<br>

严格来说定型数组不是数组，因为它们不继承自Array，但它们看起来确实很像数组，行为也很像。定型数组中的值属于8种不同数值数据类型中的一个，它们是基于ArrayBuffer对象构建的，用于表示一个或多个数字底层的数位。按位运算更适合用定型数组来操作，因为其不会像js数字类型的操作那样将值在多种格式间反复转换。<br>