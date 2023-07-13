---
title: '`delete`和Array.splice的区别[JavaScript]'
catalog: true
date: 2023-07-12 14:40:49
subtitle:
header-img:
tags:
categories:
- TECH
- FrontEnd
- JavaScript
---

## [`delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)

`delete` will delete the object property, but will not **reindex** the array or update its length. This makes it appears as if it is `undefined`:

```javascript
// Array
const myArray = ['a', 'b', 'c', 'd'];
myArray.length  // 4
delete myArray[0];
myArray.length  // 4  不会重新index, 所以length也不会改变

// Note that it is not in fact set to the value undefined, rather the property is removed from the array, making it appear undefined.
myArray[0];   // undefined
// The Chrome dev tools make this distinction clear by printing empty when logging the array.
myArray // [empty, "b", "c", "d"]
```

但是当`delete` Object的property时候就没有这个问题：

```javascript
// Object
const myArray = {'a': 1, 'b': 2, 'c': 3, 'd': 4};
Object.keys(myArray).length // 4
delete myArray['a']
Object.keys(myArray).length // 3

myArray['a'] // undefined
myArray // {b: 2, c: 3, d: 4}
```

## [Array.splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

`myArray.splice(start, deleteCount)` actually removes the element, reindexes the array, and changes its length.
实际上删除元素，重新索引数组，并更改其长度.

```javascript
> myArray = ['a', 'b', 'c', 'd']
  ["a", "b", "c", "d"]
> myArray.splice(0, 2)
  ["a", "b"]
> myArray
  ["c", "d"]
```

### [Array.remove of jQuery](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

John Resig, creator of jQuery created a very handy Array.remove method that I always use it in my projects.

```javascript
// Array Remove - By John Resig (MIT Licensed)
Array.prototype.remove = function(from, to) {
  var rest = this.slice((to || from) + 1 || this.length);
  this.length = from < 0 ? this.length + from : from;
  return this.push.apply(this, rest);
};
```

and here's some examples of how it could be used:

```javascript
// Remove the second item from the array
array.remove(1);
// Remove the second-to-last item from the array
array.remove(-2);
// Remove the second and third items from the array
array.remove(1,2);
// Remove the last and second-to-last items from the array
array.remove(-2,-1);
```

## 参考文章

- [MDN `delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)
- [MDN Array.splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
- [What is the difference between using the delete operator on the array element as opposed to using the Array.splice method?](https://stackoverflow.com/questions/500606/deleting-array-elements-in-javascript-delete-vs-splice)
