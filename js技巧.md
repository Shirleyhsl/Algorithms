
<!-- TOC -->

- [整数判断](#整数判断)
- [JSON数据序列化](#json数据序列化)
- [闰年判断](#闰年判断)
- [将"get-element-by-id"转化为驼峰式](#将get-element-by-id转化为驼峰式)
- [不用循环创建数组](#不用循环创建数组)
- [this指向目标对象](#this指向目标对象)
- [ES6的出重方法](#es6的出重方法)
- [多维数组扁平化去重并排序](#多维数组扁平化去重并排序)
- [浮点数比较大小](#浮点数比较大小)

<!-- /TOC -->
## 整数判断
> 数字还包括三种特殊的值：NaN、Infinity、-Infinity
```js

function isInterger(value) {
    return typeof value==="number" && isFinite(value) && value%1===0;
}
```

## JSON数据序列化
- 将某个JSON数据序列化，且序列化的时候去除那么属性，并将数组的第一个元素变为null
> stringify的第二个参数是过滤器，当过滤器是一个函数时，它接收两个参数：一个键和一个值。如果函数返回undefined，那么相应的键在序列化的过程中就会被跳过。在遍历数组的时候，在函数中也能操作键和值，但返回undefined，不会被忽略，而是被替换为null
```js
JSON.stringify(json, function(key, vaue) {
    if(key == 'name'){
        return undefined;
    }
    if(key === "0"){
        return undefined;
    }
    return value;
})
```

## 闰年判断
> 数字还包括三种特殊的值：NaN、Infinity、-Infinity
```js
function isLeapYear(year) {
    //3月第0天就是2月最后一天
    return (new Date(year,2,0)).getDate() === 29; 
}
```

## 将"get-element-by-id"转化为驼峰式
```js
var result = str.replace(/-([a-z])/g,function(match,p1,index,input) {
    return p1.toUpperCase();
})
```

## 不用循环创建数组
- 不用循环语句创建一个长度为50的数组，每个元素的值都等于它的索引
```js
var arr = new Array(51).join('1').split('').map((item,index)=> index)
```

## this指向目标对象
- 设计函数将f的this指向目标对象
```js
//方法1
function bindThis(func, oTarget) {
    return function () {
        return func.apply(oTarget, arguments);
    };
}
//方法2
function bindThis(f, oTarget) {
    return f.bind(oTarget);
}
```

## ES6的出重方法
```js
// 去除数组的重复成员
[...new Set(array)]
//去除字符串的重复成员
[...new Set('ababbc')].join('')
// "abc"
```

## 多维数组扁平化去重并排序
```js
Array.from(new Set(arr.flat(Infinity))).sort((a,b)=>{ return a-b})
```


## 浮点数比较大小
>正确的比较方法是用JavaScript提供的最小精度值：
```js
console.log( Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON);//true
```
