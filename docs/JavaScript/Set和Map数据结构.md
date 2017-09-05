#Set和Map数据结构  
目录结构  

	1.Set  
	2.WeakSet  
	3.Map   
	3.WeakMap  
##  1.Set
> ##1.Set  
**概念：类似数组，每个成员都是唯一的**  
	
	var s = new Set();
	[2,2,4,5,3,5].map(x=> s.add(x));
	for(let i of s){
		console.log(i);
	}
	//2 3 4 5
	相同的值只会出现一次  
### Set接收数组初始化  
例一  

	var set = new Set([2,3,4,5,2,3]);  
	[..set] ;
	//[2,3,4,5]  
例二
	
    var items = new Set([1,2,3,4,4,4]);
	items.size // 4  
例三  
	
	function divs() {
	  return [...document.querySelectorAll('div')];
	}
	var set = new Set(divs());
	set.size // 56

例四 数组去重  
	
	[...new Set(array)]  
### Set实例的属性  
-Set.prototype.constructor :构造函数  
-Set.prototype.size : 返回Set实例的成员总数  
### Set方法  
`-add(value)`: 添加某个值，返回Set解构本身  
`-delete(value)`: 删除某个值，返回一个布尔值，表示删除是否成功。  
`-has(value)`: 返回布尔值，表示该值是否为Set的成员。  
`-clear()`: 清除所有成员，没有返回值。  	
	
	var s = new Set();
	s.add(1).add(2).add(2);
	// 注意2被加入了两次
	
	s.size // 2
	
	s.has(1) // true
	s.has(2) // true
	s.has(3) // false
	
	s.delete(2);
	s.has(2) // false  
**Array.from()可以把Set转化为数组** 

	var items = new Set([1, 2, 3, 4, 5]);
	var array = Array.from(items);
**数组去从的另一种方法**  
	
	function dedupe(array) {
	  return Array.from(new Set(array));
	}
	dedupe([1, 1, 2, 3]) // [1, 2, 3]  

### 遍历Set  
**四个方法遍历成员**  
-`keys()`: 返回键的遍历器  
-`values()`: 返回键值的遍历器  
-`entries()`: 返回键值对的遍历器  
-`forEach()`: 使用回调函数遍历每个成员  

**（1）keys()，values()，entries()**  
  
	let set = new Set(['red', 'green', 'blue']);
	
	for (let item of set.keys()) {
	  console.log(item);
	}
	// red
	// green
	// blue
	
	for (let item of set.values()) {
	  console.log(item);
	}
	// red
	// green
	// blue
	
	for (let item of set.entries()) {
	  console.log(item);
	}
	// ["red", "red"]
	// ["green", "green"]
	// ["blue", "blue"]
  
**Set默认遍历**  
Set.protype[Symbol.iterator] === Set.prototype.value  //true  
所以循环是可以省略values，直接用for...of循环遍历Set 。  

	let set = new Set(['red', 'green', 'blue']);
	
	for (let x of set) {
	  console.log(x);
	}
	// red  green  blue  

**（2）forEach()**  
  
	let set = new Set([1, 2, 3]);
	set.forEach((value, key) => console.log(value * 2) )
	// 2
	// 4
	// 6  
**（3）遍历的应用**  
扩展运算符（`...`）**内部使用**`for...of`循环，所以也可以用于Set结构。	
	
	let set = new Set(['red', 'green', 'blue']);
	let arr = [...set];
	// ['red', 'green', 'blue'] 
	
**`...` 数组去重**

	let arr = [3, 5, 2, 2, 5, 5];
	let unique = [...new Set(arr)];
	// [3, 5, 2]
**数组的`map`和`filter`方法也可以用于Set了。**
  
	let set = new Set([1, 2, 3]);
	set = new Set([...set].map(x => x * 2));
	// 返回Set结构：{2, 4, 6}
	
	let set = new Set([1, 2, 3, 4, 5]);
	set = new Set([...set].filter(x => (x % 2) == 0));
	// 返回Set结构：{2, 4}  

**Set可以实现交集，并集和差集**  

	let a = new Set([1, 2, 3]);
	let b = new Set([4, 3, 2]);
	
	// 并集
	let union = new Set([...a, ...b]);
	// Set {1, 2, 3, 4}
	
	// 交集
	let intersect = new Set([...a].filter(x => b.has(x)));
	// set {2, 3}
	
	// 差集
	let difference = new Set([...a].filter(x => !b.has(x)));
	// Set {1}

## 2.WeakSet
> ##2.WeakSet    
**WeakSet结构和Set类似，也是不重合的集合**   
**区别** 
1.WeakSet的成员只能是对象，而不能是其他类型的值。  
2.WeakSet中的对象都是弱引用，即垃圾回收机制不考虑WeakSet对该对象的引用也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于WeakSet之中。这个特点意味着，无法引用WeakSet的成员，因此WeakSet是不可遍历的。  
  
	var ws = new WeakSet();
	ws.add(1)
	// TypeError: Invalid value used in weak set
	ws.add(Symbol())
	// TypeError: invalid value used in weak set  
	上面代码试图向WeakSet添加一个数值和Symbol值，结果报错，因为WeakSet只能放置对象。

**WeakSet结构有以下三个方法。**

`WeakSet.prototype.add(value)`：向WeakSet实例添加一个新成员。  
`WeakSet.prototype.delete(value)`：清除WeakSet实例的指定成员。  
`WeakSet.prototype.has(value)`：返回一个布尔值，  表示某个值是否在WeakSet实例之中。  
	
	var ws = new WeakSet();
	var obj = {};
	var foo = {};
	
	ws.add(window);
	ws.add(obj);
	
	ws.has(window); // true
	ws.has(foo);    // false
	
	ws.delete(window);
	ws.has(window);    // false  

**WeakSet没有size属性，没有办法遍历它的成员。**  
	
	ws.size // undefined
	ws.forEach // undefined
	
	ws.forEach(function(item){ console.log('WeakSet has ' + item)})  

## 3.Map
> ##3.Map  
**JavaScript的对象（Object），本质上是键值对的集合（Hash结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。**  
	
	var m = new Map();
	var o = {p: 'Hello World'};
	
	m.set(o, 'content')
	m.get(o) // "content"
	
	m.has(o) // true
	m.delete(o) // true
	m.has(o) // false 
上面代码使用set方法，将对象o当作m的一个键，然后又使用get方法读取这个键，接着使用delete方法删除了这个键。 

* 为构造函数，Map也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组。    
	
		var map = new Map([
		  ['name', '张三'],
		  ['title', 'Author']
		]);
		
		map.size // 2
		map.has('name') // true
		map.get('name') // "张三"
		map.has('title') // true
		map.get('title') // "Author"
* Map构造函数接受数组作为参数，实际上执行的是下面的算法。

		var items = [
		  ['name', '张三'],
		  ['title', 'Author']
		];
		var map = new Map();
		items.forEach(([key, value]) => map.set(key, value));    

* 如果对同一个键多次赋值，后面的值将覆盖前面的值。  
	
        let map = new Map();

        map
        .set(1, 'aaa')
        .set(1, 'bbb');

        map.get(1) // "bbb"

如果读取一个未知的键，则返回undefined
* 注意，只有对同一个对象的引用，Map结构才将其视为同一个键。这一点要非常小心。

        var map = new Map();

        map.set(['a'], 555);
        map.get(['a']) // undefined


**Map结构的实例有以下属性和操作方法。**  
* **1.size 属性**   
	
	let map = new Map();
	map.set('foo', true);
	map.set('bar', false);
	
	map.size // 2
* **2.set(key, value)**  

	var m = new Map();
	
	m.set("edition", 6)        // 键是字符串
	m.set(262, "standard")     // 键是数值
	m.set(undefined, "nah")    // 键是undefined 
* **3.get(key) 找不到返回undefined**
		
		var m = new Map();
	
		var hello = function() {console.log("hello");}
		m.set(hello, "Hello ES6!") // 键是函数
		
		m.get(hello)  // 

* **4.has(key)**  

		var m = new Map();

		m.set("edition", 6);
		m.set(262, "standard");
		m.set(undefined, "nah");
		
		m.has("edition")     // true
		m.has("years")       // false
		m.has(262)           // true
		m.has(undefined)     // true
* **5.delete(key) 返回true false**  

		var m = new Map();
		m.set(undefined, "nah");
		m.has(undefined)     // true
		
		m.delete(undefined)
		m.has(undefined)       // false 
* **6.clear() 清除所有成员，没有返回值**  
	  
		let map = new Map();
		map.set('foo', true);
		map.set('bar', false);
		
		map.size // 2
		map.clear()
		map.size // 0  
###Map遍历  
`keys()`：返回键名的遍历器。  
`values()`：返回键值的遍历器。  
`entries()`：返回所有成员的遍历器。  
`forEach()`：遍历Map的所有成员。  
**注意：Map的遍历顺序就是插入顺序。** 
* 实例  
	
		let map = new Map([
		  ['F', 'no'],
		  ['T',  'yes'],
		]);
		
		for (let key of map.keys()) {
		  console.log(key);
		}
		// "F"
		// "T"
		
		for (let value of map.values()) {
		  console.log(value);
		}
		// "no"
		// "yes"
		
		for (let item of map.entries()) {
		  console.log(item[0], item[1]);
		}
		// "F" "no"
		// "T" "yes"
		
		// 或者
		for (let [key, value] of map.entries()) {
		  console.log(key, value);
		}
		
		// 等同于使用map.entries()
		for (let [key, value] of map) {
		  console.log(key, value);
		}
### Map转化为数组  
**Map结构转为数组结构，比较快速的方法是结合使用扩展运算符(`...`)。**  
		
		let map = new Map([
		  [1, 'one'],
		  [2, 'two'],
		  [3, 'three'],
		]);
		
		[...map.keys()]
		// [1, 2, 3]
		
		[...map.values()]
		// ['one', 'two', 'three']
		
		[...map.entries()]
		// [[1,'one'], [2, 'two'], [3, 'three']]
		
		[...map]
		// [[1,'one'], [2, 'two'], [3, 'three']]
**结合数组的map方法、filter方法，可以实现Map的遍历和过滤（Map本身没有map和filter方法）。**  

		let map0 = new Map()
		  .set(1, 'a')
		  .set(2, 'b')
		  .set(3, 'c');
		
		let map1 = new Map(
		  [...map0].filter(([k, v]) => k < 3)
		);
		// 产生Map结构 {1 => 'a', 2 => 'b'}
		
		let map2 = new Map(
		  [...map0].map(([k, v]) => [k * 2, '_' + v])
		    );
		// 产生Map结构 {2 => '_a', 4 => '_b', 6 => '_c'}  
**Map还有一个forEach方法，与数组的forEach方法类似，也可以实现遍历;**。

		map.forEach(function(value, key, map) {
		  console.log("Key: %s, Value: %s", key, value);
		})

## 4.WeakMap

> ##4.WeakMap  
**WeakMap结构与Map结构基本类似，唯一的区别是它只接受对象作为键名（null除外），不接受其他类型的值作为键名，而且键名所指向的对象，不计入垃圾回收机制。** 

	var map = new WeakMap()
	map.set(1, 2)
	// TypeError: 1 is not an object!  报错
	map.set(Symbol(), 2)
	// TypeError: Invalid value used as weak map key 报错
 
WeakMap的设计目的在于，键名是对象的弱引用（垃圾回收机制不将该引用考虑在内），所以其所对应的对象可能会被自动回收。当对象被回收后，WeakMap自动移除对应的键值对。典型应用是，一个对应DOM元素的WeakMap结构，当某个DOM元素被清除，其所对应的WeakMap记录就会自动被移除。基本上，WeakMap的专用场合就是，它的键所对应的对象，可能会在将来消失。WeakMap结构有助于防止内存泄漏。 

	var wm = new WeakMap();
	var element = document.querySelector(".element");
	
	wm.set(element, "Original");
	wm.get(element) // "Original"
	
	element.parentNode.removeChild(element);
	element = null;
	wm.get(element) // undefined 
上面代码中，变量wm是一个WeakMap实例，我们将一个DOM节点element作为键名，然后销毁这个节点，element对应的键就自动消失了，再引用这个键名就返回undefined。		
### WeakMap 与Map区别  
一 是没有遍历操作（即没有key()、values()和entries()方法），也没有size属性；  
二 是无法清空，即不支持clear方法。这与WeakMap的键不被计入引用、被垃圾回收机制忽略有关。  
**因此，WeakMap只有四个方法可用：get()、set()、has()、delete()。** 

**前文说过，WeakMap应用的典型场合就是DOM节点作为键名。下面是一个例子。**
>
	let myElement = document.getElementById('logo');
	let myWeakmap = new WeakMap();
>	
	myWeakmap.set(myElement, {timesClicked: 0});
>	
	myElement.addEventListener('click', function() {
	  let logoData = myWeakmap.get(myElement);
	  logoData.timesClicked++;
	  myWeakmap.set(myElement, logoData);
	}, false);  
上面代码中，myElement是一个DOM节点，每当发生click事件，就更新一下状态。我们将这个状态作为键值放在WeakMap里，对应的键名就是myElement。一旦这个DOM节点删除，该状态就会自动消失，不存在内存泄漏风险。  
**WeakMap的另一个用处是部署私有属性。**

	let _counter = new WeakMap();
	let _action = new WeakMap();
	
	class Countdown {
	  constructor(counter, action) {
	    _counter.set(this, counter);
	    _action.set(this, action);
	  }
	  dec() {
	    let counter = _counter.get(this);
	    if (counter < 1) return;
	    counter--;
	    _counter.set(this, counter);
	    if (counter === 0) {
	      _action.get(this)();
	    }
	  }
	}
	
	let c = new Countdown(2, () => console.log('DONE'));
	
	c.dec()
	c.dec()
	// DONE
上面代码中，Countdown类的两个内部属性_counter和_action，是实例的弱引用，所以如果删除实例，它们也就随之消失，不会造成内存泄漏