`console`对象在前端调试中必不可少，但是大多数人都只会用`console`对象的`log()`方法。但`console`对象中还有其它几个有用的方法。  
### 1.  基本字符串和json对象如下
```js
 var str = "Hello World!";
```

### 2. console.log()用太多就直接跳过了
### 3.console.group()与console.groupEnd()连用  
分组打印，下方所有console.group()与console.groupEnd()是为了更好的分组显示而写的     
```js
console.group('console.error() ');
console.log(str);
console.groupEnd('');
```


    
### 4. 打印调试信息
**console.debug()**
```js
console.group('console.debug');
console.debug(str);
console.groupEnd('');
```


**console.info()，打印一个提示信息**  
```js
console.group('console.info');
console.info(str);
console.groupEnd('');
```

**console.warn()，打印一个警告**
```js
console.group('consoel.warn()');
console.warn(str);
console.groupEnd('');
```

**console.error()，打印一个错误**  
```js
	console.group('console.error()');
	console.error(str);
	console.groupEnd('');
```


**console.assert()** 条件判断`false`打印信息**   

```js
    console.group("console.assert()");
    console.assert(false);
    console.assert(400>500,'true不会打印，false才会打印');
    console.groupEnd();
```


### 5.console.table()，把对象打印成为一个table表
	
```js
var json = {
        "item1": {"name": "张三","age": 23},
        "item2": {"name": "李四","age": 54},
        "item3": {"name": "王五","age": 34}
}
console.group("console.table()");
console.table(json);
console.groupEnd();
```

**console.dir()打印对象**
```js
	console.group("console.dir()");
    console.dir(json);
    console.groupEnd();
```



### 6.console.time()和console.timeEnd()，这两个方法用于计时，可以算出一个操作所花费的准确时间
	
```js
	console.time("test1");
    var a = 1 + 2;
    console.timeEnd("test1");
    console.time("test2");
    var a = 1 + 2;
    console.timeEnd("test2");
```



