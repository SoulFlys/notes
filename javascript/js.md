### 六种数据类型
```
原始类型：number
         string
         boolean
         null
         undefined
对象类型：object
            Function
            Array
            Date
            ...
```

### ===
* 类型不同：直接返回false
* 类型相同：比较值
**
```javascript
null === null           //true
undefined === undefined //true
NaN === NaN             //false（NaN == NaN => false）
[1,2] === [1,2]         //false（[1,2] == [1,2] => false）
new Object() === new Object() //false（new Object() == new Object() => false）
```

### 包装对象(number/string/boolean都有对应的包装类型)
```javascript
var str = "hello";
var strObj = new String("hello");

str == strObj   //true
str === strObj  //false
str.length      // => 6
str.t = 10
str.t           // => undefined

(123).toString() // => new Number(123) => new Number(123).toString() => "123"
```

### 类型检测(后面单独领出来，详细学习)
```javascript
typeof
instanceof
Object.propotype.toString
constructor
duck type
```

### 运算符
```javascript
var a = (1,2,3); // => 3

var b = {x:1};
b.x         // => 1
delete b.x  
b.x         // => undefined

var obj = {};
Object.defineProperty(obj, 'x', {
    configurable: false,
    value: 1
});
delete obj.x;   // => false
obj.x       // => 1
// delete 只能删除configurable为true的属性

window.x = 1;
'x' in window // => true
```

### get/set

### Array
```javascript
new Array(10)   // undefined*10     [,,,,,,,,,,]
new Array(true, null, 1, 'hi')  // [true, null, 1, 'hi']

var arr = [1, 2, 3];
delete arr[0]
arr[0]      // undefined
arr.length  // 3
arr         // [,2,3]
```

### 稀疏数组
```javascript
0 in [undefined]    // => true
0 in new Array(1)   // => false
0 in [,,]           // => false
```

### Array 方法
* push/unshift/pop/shift
```javascript
var arr = [1, 2];
arr.push(3)         // => 返回添加后的长度 [1, 2, 3]         在尾部添加
arr.unshift(0)      // => 返回添加后的长度 [0, 1, 2, 3]      在头部添加
arr.pop()           // => 返回删除元素的值3 => [0, 1, 2]     删除尾部元素
arr.shift()         // => 返回删除元素的值0 => [1, 2]        删除头部元素
```

* 数组拼接
```javascript
arr.join()          // => "1,2"
arr.join('|')       // => "1|2"
```

* 数组反转
```javascript
arr.reverse()       // => [原数组也会被修改] => [2, 1]
```

* 数组排序
```javascript
var arr = [13, 24, 51, 3];
arr.sort()          // => [原数组也会被修改] => [13, 24, 3, 51]
arr.sort(function(a, b) {
    return a - b            // => [3, 13, 24, 51]
})
```

* 数组合并
```javascript
var arr = [1, 2, 3]
arr.concat(4, 5)            // => [1, 2, 3, 4, 5];
arr                         // => [原数组不会被修改] => [1, 2, 3]
arr.concat([10, 11], 13)    // => [1, 2, 3, 10, 11, 13]
arr.contac([1, [2, 3]])     // => [1, 2, 3, 1, [2, 3]]
```

* 返回部分数组
```javascript
var arr = [1, 2, 3, 4, 5]
arr.slice(1, 3)             // => [原数组不会被修改] => [2, 3]
arr.slice(1)                // => [2, 3, 4, 5]
arr.slice(1, -1)            // => [2, 3, 4]
arr.slice(-4, -3)           // => [2]
```

* 数组删除
```javascript
var arr = [1, 2, 3, 4, 5]
arr.splice(2)               // => [3, 4, 5]
arr                         // => [原数组也会被修改] => [1, 2]
var arr = [1, 2, 3, 4, 5]
arr.splice(2, 2)            // => [3, 4]
arr                         // => [1, 2, 5]
var arr = [1, 2, 3, 4, 5]
arr.splice(1, 1, 'a', 'b')  // => [2]
arr                         // => [1, 'a', 'b', 3, 4, 5]
```

* 数组遍历（以下都是ES5新加的）
```javascript
var arr = [1, 2, 3, 4, 5]
arr.forEach(function(x, index, a){
    console.log(x + "|" + index + "|" + (a === arr))
})
// 1|0|true
// 2|1|true
// 3|2|true
// 4|3|true
// 5|4|true
```

* 数组映射
```javascript
var arr = [1, 2, 3]
arr.map(function(x){
    return x + 10
})                  // => [11, 12, 13]
arr                 // => [1, 2, 3]
```

* 数组过滤
```javascript
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
arr.filter(function(x, index){
    return index % 3 === 0 || x >= 8
})                  // => [1, 4, 7, 8, 9, 10]
arr                 // => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

* 数组判断
```javascript
var arr = [1, 2, 3, 4, 5]
arr.every(function(x){return x < 10})   // => [检测数组所有元素是否都符合指定条件] => true
arr.every(function(x){return x < 3})    // => false
arr.some(function(x){return x === 3})   // => [检测数组中的元素是否满足指定条件] => true
arr.some(function(x){return x === 100}) // => false
```

* reduce/reduceRight
```javascript
var arr = [1, 2, 3]
var sum = arr.reduce(function(x, y){
    return x + y
}, 3)               // => 3+1+2+3 => 9
arr                 // => [1, 2, 3]
var sum = arr.reduce(function(x, y){
    return x + y
})                  // => 1+2+3  => 6
var arr = [3, 9, 6]
var max = arr.reduce(function(x, y){
    console.log(x + '|' + y);
    return x > y ? x : y;
})
// 3|9
// 9|6
max;    // => 9
var max = arr.reduceRight(function(x, y){
    console.log(x + '|' + y);
    return x > y ? x : y;
})
// 6|9
// 9|3
max;    // => 9
```

* 数组检索indexOf/lastIndexOf
```javascript
var arr = [1, 2, 3, 2, 1]
arr.indexOf(2)          // => 1
arr.indexOf(99)         // => -1
arr.indexOf(1, 1)       // => 4 从第二个元素查找
arr.indexOf(1, -3)      // => 4
arr.indexOf(2, -1)      // => -1
arr.lastIndexOf(2)      // => 3 从右向左找 返回的都是下标
arr.lastIndexOf(2, -2)  // => 3
arr.lastIndexOf(2, -3)  // => 1
```

* 判断是否是数组isArray
```javascript
Array.isArray([])           // => true
[] instanceof Array         // => true
[].constructor === Array    // => true
({}).toString.apply([]) === '[object Array]'    // => true
```

### 函数
* apply/call/bind(bind是ES5新增)
    * apply() 调用一个函数, 其具有一个指定的this值，以及作为一个数组（或类似数组的对象）提供的参数【一个包含多个参数的数组】
    * call()  调用一个函数, 其具有一个指定的this值和分别地提供的参数(参数的列表)【若干个参数的列表】
    * bind()  创建一个新的函数, 当被调用时，将其this关键字设置为提供的值，在调用新函数时，在任何提供之前提供一个给定的参数序列。
```javascript
    var o = {a: 1, b: 3}
    function add(c ,d) {
        return this.a + this.b + c + d
    }
    add.call(o, 5, 7)       // => 1+3+5+7
    add.apply(o, [5, 7])    // => 1+3+5+7

    function bar() {
        console.log(Object.prototype.toString.call(this))
    }
    bar.call(7)          // => [object Number]
```
```javascript
    function cat(){}
    cat.prototype = {
        food: "fish",
        say: function() {
            console.log("I love "+this.food);
        }
    }
    var blackCat = new cat;
    blackCat.say();             // => I love fish

    //但是如果我们有一个对象
    var whiteDog = {food: "bone"} //我们不想对它重新定义say方法，
    //那么我们可以通过call或apply用blackCat的say方法：
    blackCat.say.call(whiteDog)  // => I love bone
    blackCat.say.apply(whiteDog) // => I love bone
```
```javascript
    //bind方法的返回值是函数
    var x = 20;
    var obj = {
        x: 42,
        getX: function() {
            return this.x;
        }
    }

    var retrieveX = obj.getX;
    console.log(retrieveX());       // => 20

    var boundGetX = retrieveX.bind(obj);
    console.log(boundGetX());       // => 42

    var o = {a: 1}
    var p = {a: 2}
    var func = function() {
        return this.a;
    }
    func.bind(o)();     // => 1
    func.bind(p)();     // => 2
```
