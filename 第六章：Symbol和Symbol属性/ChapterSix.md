## 第六章：Symbol和Symbol属性

1、es6提供了一个可以随时访问的全局Symbol注册表；<br>
Symbol.for()方法首先在全局Symbol注册表中搜索键为“uid”的Symbol是否存在，如果存在直接返回已有的Symbol；否则创建一个新的Symbol，并使用这个键在Swmbol全局注册表中注册，随即返回新创建的Symbol。<br>

2、Symbol属性检索<br>
Object.keys()方法和Object.getOwnPropertyNames()方法可以检索对象中的所有属性名；前一个方法返回所有可枚举的属性名，后一个方法不考虑属性的可枚举性一律返回。而es6中增加了Object.getOwnProperty-Symbols()方法来检索对象中的Symbol属性；<br>Object.getOwnProperty-Symbols()方法的返回值是一个包含所有Symbol自有属性的数组。<br>
Symbol仍然可以通过Object.definePorperty()和Object.defineProperties()来改变它们；<br>