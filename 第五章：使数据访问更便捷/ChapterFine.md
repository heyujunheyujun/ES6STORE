## 第五章：使数据访问更便捷

嵌套解构赋值<br>
let node = {<br>
  type: 'string',<br>
  name: 'nora',<br>
  loc: {<br>
    start: {<br>
      line: 1<br>
    }<br>
  }<br>
}<br>
let {loc: {start}} = node;<br>
console.log(start.line); // 1<br>

数组解构<br>
let colors = ['red', 'green', 'blue'];<br>
let [ , , thirdColor] = colors;<br>
console.log(thirdColor); // blue  按顺序赋值<br>

无临时变量的数组交换<br>
let a = 1;<br>
let b = 2;<br>
[a, b] = [b, a];<br>

复制数组<br>
es5: var cloneColors = colors.concat();<br>
es6: let [...cloneColors] = colors;<br>