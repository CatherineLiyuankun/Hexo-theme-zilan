---
title: JavaScript比较两个Array数组/Object的内容是否相同
catalog: true
date: 2020-02-04 18:17:01
subtitle: Compare Array or Object
header-img:
tags:
- Array
categories:
- TECH
- FrontEnd
- JS
---
# Why can not use === to compare Array?
复习下javascript包括两个不同类型的值， 最新的 ECMAScript 标准定义了 8 种数据类型:
- 基本数据类型(7种原始类型): 是按值访问的, 保存在栈内存（Stack）里, 基本类型的值是不可变的, 基本类型的比较是它们的值的比较。
    - Boolean
    - Null
    - Undefined
    - Number
    - BigInt
    - String
    - Symbol 
- 引用数据类型 (1种Object类型): 按引用访问的, 保存在堆内存(Heap)中的对象, 引用类型的值是可变的, 引用类型的比较是引用的比较。
    - Object
    - Array
    - Function
    - 正则（RegExp）
    - 日期（Date）

```javascript
var a = 1;
var b = a;
b = 2;
console.log(a);  // 1
```

b获取的是a值的一份拷贝，虽然两个变量的值相等，但是两个变量保存了两个不同的基本数据类型值。b只是保存了a赋值的一个副本，所以，b的改变，对a没有影响。

```javascript
var obj1 = [];    // 新建一个空数组 obj1
var obj2 = [];    // 新建一个空数组 obj2
console.log(obj1 == obj2);    // false
console.log(obj1 === obj2);   // false
```
因为 obj1 和 obj2 分别引用的是存放在堆内存中的2个不同的对象，故变量 obj1 和 obj2 的值（引用地址）也是不一样的
==或===操作符只能比较两个对象是否是同一个实例，也就是是否是同一个对象引用。目前JavaScript没有内置的操作符判断对象的内容是否相同。

# How to compare Array?
## Method 1 Transform Array toString
```javascript
 array1.toString() === array2.toString()
 // or
 JSON.stringify(array1) === JSON.stringify(array2)
```
不推荐，原因：
- 首先要保证两个数组顺序一致，例如[1, 2] [2, 1] 顺序不一致，但内容相同。
- 其次，不是因为转换成字符串类型后才相等。
例如array1=[1, 2], array1=['1', '2'];
array1.toString() === array2.toString() // true
- 简单数组['1', '2']，不是嵌套数组['1', '2', ['1', '2']]

## Method 2 For string[]
如果保证：
- 不是因为转换成字符串类型后才相等。
例如array1=[1, 2], array1=['1', '2'];
array1.toString() === array2.toString() // true
- 简单数组['1', '2']，不是嵌套数组['1', '2', ['1', '2']]

```javascript
// funtion for simple array string[]
isArrayEquals(array1, array2) {
    if(!(array1 || array1)) {
      return false;
    }
    // Compare the length
    if (array1.length != array2.length) {
        return false;
    }
    // 先排序再转化为string比较
    if (array1.sort().toString() === array2.sort().toString()) {
    // if (JSON.stringify(array1.sort()) === JSON.stringify(array2.sort()) ) {
        return true;
    }
    return false;
}
```

## Method 3 For all kinds of array
适应任何array, 包括嵌套数组。

for all kinds of array

```javascript
// prototype 方法
// Warn if overriding existing method
if (Array.prototype.equals) {
    console.warn("Overriding existing Array.prototype.equals. Possible causes: New API defines the method, there's a framework conflict or you've got double inclusions in your code.");
}

Array.prototype.equals = function(array) {
  if (!array) {
    return false;
  }
  if (this.length !== array.length) {
    return false;
  }
  for (var i = 0; i < this.length; i++) {
    if (this[i] instanceof Array && array[i] instanceof Array) {
      if (!this[i].equals(array[i])) {
        return false;
      }
    }
    else if (this[i] !== array[i]) {
      return false;
    }
  }
  return true;
}
```

```javascript
// funtion for all kinds of array
isArrayEquals(array1, array2) {
    if(!(array1 || array1)) {
      return false;
    }
    // Compare the length
    if (array1.length != array2.length) {
        return false;
    }

    for (var i = 0; i < array1.length; i++) {
        // check wheather it's nested arrays
        if (array1[i] instanceof Array && array2[i] instanceof Array) {
            // Recursion
            if (!isArrayEquals(array1[i],array2[i]))
                return false;       
        } else if (this[i] != array[i]) {
            return false;   
        }           
    }       
    return true;
}
```

# How to compare Object?
那么同样的道理怎么比较Object呢？
```javascript
Object.prototype.equals = function(object2) {
    //For the first loop, we only check for types
    for (propName in this) {
        //Check for inherited methods and properties - like .equals itself
        //https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty
        //Return false if the return value is different
        if (this.hasOwnProperty(propName) != object2.hasOwnProperty(propName)) {
            return false;
        }
        //Check instance type
        else if (typeof this[propName] != typeof object2[propName]) {
            //Different types => not equal
            return false;
        }
    }
    //Now a deeper check using other objects property names
    for (propName in object2) {
        //We must check instances anyway, there may be a property that only exists in object2
            //I wonder, if remembering the checked values from the first loop would be faster or not 
        if (this.hasOwnProperty(propName) != object2.hasOwnProperty(propName)) {
            return false;
        }
        else if (typeof this[propName] != typeof object2[propName]) {
            return false;
        }
        //If the property is inherited, do not check any more (it must be equa if both objects inherit it)
        if(!this.hasOwnProperty(propName))
          continue;

        //Now the detail check and recursion

        //This returns the script back to the array comparing
        /**REQUIRES Array.equals**/
        if (this[propName] instanceof Array && object2[propName] instanceof Array) {
                   // recurse into the nested arrays
           if (!this[propName].equals(object2[propName]))
                        return false;
        }
        else if (this[propName] instanceof Object && object2[propName] instanceof Object) {
                   // recurse into another objects
                   //console.log("Recursing to compare ", this[propName],"with",object2[propName], " both named ""+propName+""");
           if (!this[propName].equals(object2[propName]))
                        return false;
        }
        //Normal value comparison for strings and numbers
        else if(this[propName] != object2[propName]) {
           return false;
        }
    }
    //If everything passed, let's say YES
    return true;
}
```


## Reference Links
- [JavaScript 数据类型和数据结构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures)
- [JavaScript 深入了解基本类型和引用类型的值](https://segmentfault.com/a/1190000006752076)
