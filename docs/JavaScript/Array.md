
### Array.from()  把类似数组转换为真正的数组

```js
    Array.form(oli)
```
### arr.forEach  循环遍历

```js
	arr.forEach( function(item){
		console.log(item)
	})
```
### Array.of 将一组值转换为数组

	Array.of(1,2,3) //[1,2,3]
### Array.copyWithin() 指定成员复制到其他位置

```js
	Array.prototype.copyWithin(target,start,end)
	target: 覆盖目标开始位置
	start: 要复制的开始位置
	end: 要复制的结束位置
```
### find()  过滤查找

```js
	[1,2,3,4,5,6].find(function(value,index,arr){
		return value>3 ;
	}) //[4,5,6]
```
### findIndex 返回元素存在的位置
### Array.fill(5) 使用给定值填充一个数组

```js
	new Array(3).fill(5) //[5,5,5]
	['a','b','c'].fill(7,1,2) //['a',7,'c']
	(value, start, end)
```
### entries(), keys()和values() 用于遍历数组

```js
	for (let index of ['a', 'b'].keys()) {
	  console.log(index);
	}
	// 0
	// 1
	for (let elem of ['a', 'b'].values()) {
	  console.log(elem);
	}
	// 'a'
	// 'b'
	for (let [index, elem] of ['a', 'b'].entries()) {
	  console.log(index, elem);
	}
	// 0 "a"
	// 1 "b"
```

>**如果不使用for...of循环，可以手动调用遍历器对象的next方法，进行遍历。**  

```js
	let letter = ['a', 'b', 'c'];
	let entries = letter.entries();
	console.log(entries.next().value); // [0, 'a']
	console.log(entries.next().value); // [1, 'b']
	console.log(entries.next().value);
```
### includes 数组实例  返回布尔值，数组是否包含给定值

```js
	[1,3,4].includes(3); //true
	[1,3,4].includes(6); //false
	[1,3,NaA].inclucdes(NaN); //true
```
>**第二个参数表示搜索起始的位置**    

```js
	[1, 2, 3].includes(3, 3);  // false
	[1, 2, 3].includes(3, -1); // true
```
### 数组的空位

	Array(3) //[,,,]
**上面代码中，Array(3)返回一个具有3个空位的数组。**    
**空位不是undefined，一个位置的值等于undefined，依然是有值的。空位是没有任何值，in运算符可以说明这一点。**

```js
	0 in [undefined, undefined, undefined] // true
	0 in [, , ,] // false
```

**ES6则是明确将空位转为undefined。**


Array.from方法会将数组的空位，转为undefined，也就是说，这个方法不会忽略空位。  

```js
	Array.from(['a',,'b'])
	// [ "a", undefined, "b" ]
```

扩展运算符（...）也会将空位转为undefined。

```js
	[...['a',,'b']]
	// [ "a", undefined, "b" ]
```

copyWithin()会连空位一起拷贝。
	[,'a','b',,].copyWithin(2,0) // [,"a",,"a"]
fill()会将空位视为正常的数组位置。

```js
new Array(3).fill('a') // ["a","a","a"]
```

  

**entries()、keys()、values()、find()和findIndex()会将空位处理成undefined**   
##由于空位的处理规则非常不统一，所以建议避免出现空位
