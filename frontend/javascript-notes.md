# JavaScript笔记



**js中一切皆对象**

## 第一部分：JS基础语法与表达式

### 一、基础语法与变量

#### 1、JavaScript书写位置，有两个

- 可以在body标签中的script标签内书写
- 书写单独js文件，再src引入

#### 2、输出语句：

- alert()  - 在网页弹出一个警告框
  - alert('你好，这是网页提示信息');
- console.log()  - 控制台输出



> 控制台：也是一个REPL环境，可以使用它临时测试表达式的值
>
> REPL：read读--eval执行--print打印--loop循环

#### 3、变量：

用关键字 var 定义，如： var a

用=等号赋值，如：var a = 10

只定义没有赋值的变量，默认值是undefined

#### 4、总结：重点内容

- JavaScript在哪里书写，在哪里运行？
- JavaScript有哪些输出语句？
- 变量是什么？如何定义变量？变量的合法命名规则有哪些？
- 只有var定义一个变量，但没有赋初值，这个变量的值是？
- 什么是变量声明的提升？
- JavaScript中，等号的功能是什么？

### 二、基本数据类型

使用typeof运算符检测数据类型

#### 1、基本数据类型种类

Number(数字类型)、String(字符串类型)、Boolean(布尔类型)、Undefined、Null

##### Number(数字)类型

所有数字不分大小、不分整浮、不分正负都是数字类型。

- 二进制数值以0b开头
- 八进制数字以0开头
- 十六进制数字以0x开头

特殊的数字型值NaN，它是一个数字类型的值，它不自等。

- typeof NaN  // "number"
- NaN == NaN  // false

##### String(字符串)类型

可以用+加号拼接

字符串的length属性表示字符串的长度

charAt()方法可以得到指定位置的字符

substring(a,b)方法得到从a开始到b(不包含b处位)结束的子串，省略第二个参数将默认到结尾。可以自动交换两个参数位置

substr(a,b)方法将得到从a开始的长度为b的子串，省略第二参数将默认到结尾。a可以是负数，表示倒数位置。

slice(a,b)方法得到从a开始到b结束(不包含b处位)的子串，参数a可以是负数。参数a必需小于参数b。

toUpperCase()转为大写

toLowerCase()转为小写

indexOf()方法返回某个指定字符串值再字符串中首次出现的位置，没有出现则返回-1

##### null 类型

null表示空，它是“空对象”

#### 2、数据类型转换

- Number()函数 转换为数字类型

  - 字符串-->数字：纯数字字符串能变成数字，不是纯数字的字符串转为NaN
  - 布尔值-->数字：true=1，false=0
  - undefined-->数字：NaN
  - null-->数字：0

- parselnt()函数 将字符串转为整数

- parseFloat()函数 将字符串转为浮点数

- String()函数 转为字符串类型

  - 数字-->字符串 变为“长得相同”的字符串。
  - 科学计数法和非16进制数字会转为10进制的值

  常规采用.toString()方法转换


#### 3、案例：小小计算器

使用promot()函数弹出输入框，让用户输入两个数字

对用户输入的两个数字进行加法运算，而由于用户输入的内容是字符串类型，所以必须先转为数字类型，再运算。

```javascript
// 用户输入两个数字
var a = Number(prompt('请输入第一个数字：'));
var b = Number(prompt('请输入第二个数字：'));
// 计算两个数字和
var sum = a +b;
// 
alert('结果是：' +sum);
```



#### 4、复杂数据类型（拓展）

Object、Array、Function、RegExp、Date、Map、Set等等

#### 5、总结：重点内容

- JavaScript中有那些基本类型值？它们的typeof检测结果是什么
- NaN、undefined、null的特殊值是什么？
- 各种类型值相互转换的方法和转换规律
- substring()、substr()和slice()方法的使用及区别要掌握及熟记

### 三、表达式与操作符

算术表达式、逻辑表达式、关系表达式

隐式类型转换

如果参与数学运算的某操作数不是数字型，那么js会自动将此操作数转换为数字型。隐式转换的本质式内部调用Number()函数。

#### 1、赋值表达式



#### 2、逻辑表达式

优先级：非 --> 与 --> 或

#### 3、综合表达式

优先级：非运算 --> 数学运算 --> 关系运算 --> 逻辑运算

#### 4、有关IEEE754

在javaScript中，有些小数的数学运算不是很精准，JavaScript使用了IEEE754二进制浮点数算术标准，这会使一些个别的小数运算产生“丢失精度”问题。

解决方法：在进行小数运算时，要调用数字的**toFixed()**方法保留指定的小数位数。

`Number((0.1+0.2).toFixed(2))`   // 0.30

#### 5、总结：重点内容

- 表达式有哪几种？每种表达式分别有哪些运算符？
- 每种表达式中运算顺序是什么？综合运算顺序是什么？
- 什么是短路计算？3&&13和3||13的结果分别是什么？
- a++和++a的区别？

## 第二部分、流程控制语句与数组

### 一、流程控制语句

#### 1、条件语句

##### if 语句

if语句最简单的条件语句，也称选择语句。

if(条件){

​	语句块(条件为真，执行这里)

}else {

​	语句块(条件为假，执行这里)

}

##### 案例：

###### 水仙花数

水仙花数是这样的一个3位数：它的每个数位的数字的立方和等于它本身。

```js
// 要求用户输入一个三位数
var n = Number(prompt('请输入一个三位数'));

// 对用户输入的数值，进行合法性的验证
if (!isNaN(n) && 100 <= n && n <= 999) {
	// 当用户输入的数字是合法
    
	// 字符串方法
	// 把数字n变为字符串
	// var n_str = n.toString();
	// 个位
	// var a = Number(n_str.charAt(2));
	// 十位
	// var b = Number(n_str.charAt(1));
	// 百位
	// var c = Number(n_str.charAt(0));
    
	// 数学方法
	// 百位
	var a = Math.floor(n / 100);
	// 十位
	var b = Math.floor(n / 10) % 10;
	// 各位
	var c = n % 10;

	// 根据水仙花数的条件进行判断
	if (Math.pow(a, 3) + Math.pow(b, 3) + Math.pow(c, 3) == n) {
		alert('这个数字是水仙花数');
	} else {
		alert('这个数字不是水仙花数');
	}
} else {
	// 输入不合法
	alert('您输入的数字不合法的');
}
```

###### 游乐园门票

某游乐园的门票价格如下表所示。请根据用户输入的年龄和星期几，弹出对话框显示门票价格。

|      | 年龄大于等于10岁 | 年龄小于10岁 |
| ---- | ---------------- | ------------ |
| 平日 | 300              | 140          |
| 周末 | 500              | 210          |

```javascript
// 让用户输入星期几
var week = Number(prompt('请输入星期几'));
// 再让用户输入年龄
var age = Number(prompt('请输入年龄'));

// 让星期几作为大前提条件
if (week == 0 || week == 6) {
	// 周末
	if (age >= 10) {
		alert(500);
	} else {
		alert(210);
	}
} else {
	// 平日
	if (age >= 10) {
		alert(300);
	} else {
		alert(140);
	}
}
```

##### switch 语句

当一个变量被分类讨论的情形

```javascript
// 让用户输入年份
var year = Number(prompt('请输入一个年份'));
// 让用户输入一个月份
var month = Number(prompt('请输入一个月份'));

// 根据月份来分类讨论
switch (month) {
	case 1:
	case 3:
	case 5:
	case 7:
	case 8:
	case 10:
	case 12:
		alert('这个月有31天');
		break;
	case 4:
	case 6:
	case 9:
	case 11:
		alert('这个月有30天');
		break;
	case 2:
		// 根据用户输入的year计算一下当年是不是闰年
		if (year % 4 == 0 && year % 100 != 0 || year % 100 == 0 && year % 400 == 0) {
			// 满足闰年的条件
			alert('这个月有29天');
		} else {
			alert('这个月有28天');
		}
		break;
	default:
		alert('你输入的月份有误');
}
```

switch语句并不像if语句那样当执行了某一个分支之后会自动跳出if语句体，程序员必须主动调用break来跳出switch语句体。如果不书写break，则后面的所有case都会被视为匹配，知道遇见break。

##### break 语句

break表示立即终止循环，它只能用在循环语句中，在for循环和while循环中都可以使用

##### continue 语句

continue用于跳过循环中的一个迭代，并继续执行循环中的下个迭代。for循环更经常使用continue。

##### 三元运算符

条件表达式 ? 表达式1 : 表达式2

#### 2、循环语句

##### for循环语句

for(表达式1;表达式2;表达式3){循环体}

- 表达式1：循环开始前执行，初始化循环所用变量
  - 可选，也可初始化多个值
- 表达式2：定义运行循环的条件，满足循环继续，否则循环结束
  - 可选，如省略那么必须循环内提供break，否则循环无法停止。
- 表达式3：每次循环体后执行的代码，增量或减量。
  - 可选，如循环内部有相应增量代码时可省略。

```javascript
// 寻找1~100当中的既能被3整除，也能被5整除的数字
// 穷举法，从1开始试验
for (var i = 1; i <= 100; i++) {
	if (i % 3 == 0 && i % 5 == 0) {
		console.log(i);
	}
}
```

##### while循环语句

while语句是一种”不定范围“循环

while(条件){循环体}

当条件满足，就会一直执行循环语句块

```javascript
// 累加1+2+3+4+……100
// 累加器
var sum = 0;
// 循环变量
var i = 1;
while (i <= 100) {
	sum += i;
	i++;
}
console.log(sum);
```

##### do while 循环

是后测试循环语句

```js
do {
	循环体
} while (循环执行条件)
```

##### 随机数函数

Math.random()

##### 案例

###### 猜数字小游戏

随机生成一个2到99的数字，让用户猜测这个数字

```javascript
// 随机一个数字，2~99之间
var answer = parseInt(Math.random() * 98) + 2;
// 此时范围的最小值和最大值，这个数值是用来提示用户的
var min = 1;
var max = 100;

do {
	// 询问用户猜测的数字
	var n = Number(prompt('请猜测数字' + min + '~' + max));
	// 验证用户输入的数字是否在范围内
	if (n <= min || n >= max) {
		alert('你输入的数字不在范围内');
		// 不在区间内，直接放弃这次循环，就开启下一次迭代
		continue;
	}

	// 判断用户输入的数字和answer的关系
	if (n > answer) {
		alert('你输入的数字太大了');
		// 因为用户输入的数字较大，所以可以让此时的最大范围数字变为用户输入的值
		max = n;
	} else if (n < answer) {
		alert('你输入的数字太小了');
		// 因为用户输入的数字较小，所以可以让此时的最小范围数字变为用户输入的值
		min = n;
	}
} while (n != answer);

// 出了do while循环，就说明n和answer相等了，因为只有相等了，才能出循环。
alert('恭喜猜对了！');
```

#### 3、算法

算法(Algorithm)是指解题方案的准确而完整的描述，是一系列解决问题的清晰指令，算法代表着用系统的方法描述解决问题的清晰指令，算法代表着用系统的方法描述解决问题的策略机制。也就是说，能够对一定规范的输入，在有限时间内获得所要求的输出。

算法就是把一个问题，拆解为计算机能够一步一步不执行的步骤。

计算机的流程控制语句：顺序执行，选择语句，循环语句

优秀算法的要求：正确性、健壮性、可读性

##### 累加器&&累乘器

###### 累加分数和

```javascript
// 由用户输入数字n，计算3/2 + 4/3 + 5/4 + …… + (n+1)/n的结果

// 用户输入数字n
var n = Number(prompt('请输入数字n'));

// 累加器
var sum = 0;

// 遍历分母就可以了，因为分母就是分子加1有关系
for (var i = 2; i <= n; i++) {
	sum += (i + 1) / i;
}

alert(sum.toFixed(2));
```

###### 计算阶乘

```javascript
// 计算阶乘

// 请用户输入数字n
var n = Number(prompt('请输入数字'));

// 累乘器，一定注意，累乘器要从1开始，因为如果从0开始，0乘以任何数字都是0,
var result = 1;

// 倒着遍历，计算阶乘
for (var i = n; i >= 1; i--) {
	result *= i;
}

// 显示结果
alert(result);
```

###### 莱布尼茨级数估算圆周率

```javascript
// 用莱布尼茨级数估算圆周率
// π = 2 * (1 + 1/3 + (1*2)/(3*5) + (1*2*3)/(3*5*7) + (1*2*3*4)/(3*5*7*9) + (1*……n)/(3*5*……2n+1))

// 累加器，就是最后的答案，
var sum = 0;
// 累乘器，用来制作每一项，制作出来的这个项，要往累加器中累加
var item = 1;

// 让用户输入n
var n = Number(prompt('请输入数字n'));

// 遍历
for(var i = 1 ; i <= n ; i++){
	// 要先制作出这一项，这一项怎么制作？要使用累乘器。item就是小车厢。
	item *= i / (2 * i + 1);
	// console.log(item);
	// 把车厢往累加器中累加
	sum += item;
}

// 显示结果
alert((1 + sum) * 2);
```

##### 穷举法

计算机最突出的能力就是计算，它没有归纳总结、逻辑推理的能力。所以人们使用计算机解决问题的时候，要”扬长避短“--充分发挥计算机的计算优势，而不要让它进行逻辑推理。穷举法就是这样的一种算法思想。

##### 综合案例

##### 

#### 4、总结：重点内容-⭐⭐⭐⭐⭐

- JavaScript中的流程控制语句有哪些？
- if多分支语句的执行机理？for循环的执行机理
- 累加器和累乘器、穷举法算法思想
- 各种算法题目
- 此部分知识点，需要融会贯通，转化为内功，多理解反复练习

### 二、数组

数组(Array),顾名思义，用来存储一组相关的值，从而方便进行求和，计算平均数，逐项遍历等操作。

#### 1、定义方法

- 数组的定义方法1：var arr = [96,96,97,91]; 
- 数组的定义方法2：var arr = new Array(96,96,97,91); 
- 数组的定义方法3：var arr = new Array(4); 
  - 表示定义了一个长度为4的数组，4项元素值为undefined

#### 2、数组的length属性

length属性获取数组的长度

#### 3、更改数组项

数组并不是只读的，可以修改其中任何项的值

如果更改的数组项超过了length-1，则会创造这个项

var arr = [2,6,7,3];

arr[6] = 4;

console.log(arr)

[2,6,7,3,empty * 2, 4]

#### 4、数组类型的检测

数组用typeof检测结果是object

Array.isArray(obj)方法可以用来检测数组

语法：

Array.isArray(obj)

参数obj,必填项，是要判断的对象，如果是返回true,否则返回false

#### 5、数组的常用法

##### 数组的头尾操作

| 方法      | 功能                                 |
| --------- | ------------------------------------ |
| push()    | 在尾部插入新项                       |
| pop()     | 在尾部删除最后一项，可以返回删除的值 |
| unshift() | 在头部插入新项                       |
| shift()   | 在头部删除第一项，可以返回删除的值   |

##### splice()方法

- 用于替换数组中的指定项

  ```js
  var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
  arr.splice(3, 2, 'X', 'Y', 'Z'); // 从下标3的项开始，连续替换2项
  console.log(arr)
  // ['A', 'B', 'C', 'X', 'Y', 'Z', 'F', 'G']
  ```

- 用于在指定位置插入新项.

  ```js
  var arr = ['A', 'B', 'C', 'D'];
  arr.splice(2, 0, 'X', 'Y', 'Z'); // 从下标2的项开始，替换0项
  console.log(arr)
  // ['A', 'B', 'X', 'Y', 'Z', 'C', 'D']
  ```

- 用于删除指定项

  ```js
  var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
  arr.splice(2, 4); // 没有设置替换的新项，仅删除4项
  console.log(arr)
  // ['A', 'B', 'G']
  ```


##### slice() 方法

- 用于得到子数组，类似于字符串的slice()方法

- slice(a, b)截取的子数组从下标a的项开始，到下标b(但不包括下标b项)结束。

- slice(a, b)方法不改变原数组

- 第二个参数可以省略，省略后将默认截取到末尾

- 参数允许为负数，表示数组的倒数第几项

  

##### join() 方法

- join()方法可以将数组转为字符串
- join()的参数表示以什么字符作为连接符，留空则默认为以逗号分隔。

##### split() 方法

- split()方法可以使字符串转为数组
- split()的参数 表示以什么字符拆分字符串，不能留空

##### concat() 方法

- concat()方法可以合并连接多个数组

  ```js
  var arr01 = [1, 2, 3, 4];
  var arr02 = [5, 6, 7];
  var arr03 = [8, 9, 10];
  var arr = arr01.concat(arr02, arr03);
  console.log(arr);
  //  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  ```

- concat()方法不改变原数组

##### reverse() 方法

用来将一个数组中的全部项顺序置反

##### indexOf() 方法

indexOf()方法是搜索数组中的元素，并返回它所在的位置，如果元素不存在，则返-1。

##### includes() 方法

includes()方法是判断一个数组是否包含一个指定的值，返回布尔值。

#### 6、数组遍历

##### 元素值的总和、平均数

```js
// 求数组的总和和平均数
var arr = [3, 5, 3, 2, 1, 1];
// 累加器
var sum = 0;
// 遍历数组，每遍历一个数字，就要把这个数字累加到累加器中
for (var i = 0; i < arr.length; i++) {
	sum += arr[i];
}
console.log(sum);
console.log(sum / arr.length);
```

##### 数组中元素的最大值和最小值

```js
// 求数组的最大值和最小值
var arr = [3, 4, 88, 3, 1];

// 定义两个变量，max表示当前寻找到的最大值，默认是arr[0]
//              min表示当前寻找到的最小值，默认是arr[0]
var max = arr[0];
var min = arr[0];

// 遍历数组，从下标为1的项开始遍历
for (var i = 1; i < arr.length; i++) {
	// 如果你遍历的这项，比当前最大值大，那么就让当前最大值成为这个项
	if (arr[i] > max) {
		max = arr[i];
	} else if (arr[i] < min) {
		// 否则如果你遍历的这项，比当前最小值小，那么就让当前最小值成为这个项
		min = arr[i];
	}
}
console.log(max, min);
```

##### 数组去重

思路： 创建一个新的空数组，遍历原数组的每个元素，判断元素是否在新数组中，如果没有就添加。最终获得没有重复元素的新数组

```js
var arr = [1, 1, 1, 2, 2, 3, 3, 3, 2, 1];

// 结果数组
var result = [];

// 遍历原数组
for (var i = 0; i < arr.length; i++) {
	// 判断遍历到的这项是否在结果数组中，如果不在就推入
	// includes方法用来判断某项是否在数组中
	if (!result.includes(arr[i])) {
		result.push(arr[i]);
	}
}
console.log(result);
```



##### 数组的随机样本

```js
var arr = [3, 6, 10, 5, 8, 9];

// 结果数组
var result = [];

// 遍历原数组
for (var i = 0; i < 3; i++) {
	// 随机选择一项的下标，数组的下表0~arr.length - 1;
	// 之前学习过一个random的公式，[a,b]区间的随机数是parseInt(Math.random() * (b-a+1)) + a;
	var n = parseInt(Math.random() * arr.length);
	// 把这项推入结果数组
	result.push(arr[n]);
	// 删除这项，防止重复被随机到
	arr.splice(n, 1);
}

console.log(result);
```

##### 冒泡排序

冒泡排序是一个著名的排序算法

冒泡排序的核心思路是一趟一趟的进行多次项的两两比较，每次都会将最小的元素排好位置，如同水中的气泡上浮一样。

n个数字，共需要比较n-1趟，比较次数为n(n-1)/2次。

```js
// 冒泡排序
var arr = [6, 2, 9, 3, 8, 1, 45, 23, 45, 49];

// 一趟一趟比较，趟数序号就是i
for (var i = 1; i < arr.length; i++) {
	// 内层循环负责两两比较
	for (var j = arr.length - 1; j >= i; j--) {
		// 判断项的大小
		if (arr[j] < arr[j - 1]) {
			// 这一项比前一项还小了，那么就要交换两个变量的位置
			var temp = arr[j];
			arr[j] = arr[j - 1];
			arr[j - 1] = temp;
		}
	}
	console.log(arr);
}
console.log(arr);
```

#### 7、二维数组

二维数组：以数组作为数组元素的数组，即“数组的数组”

二维数组可以看做是矩阵

```javascript
var matrix = [
	[11, 33, 36],
    [34, 31, 44, 66],
    [15, 18, 19]
];
console.log(matrix.length);

// 两次循环遍历输出二维数组每一个项
for(var i=0; i<3; i++){
    for(var j=0; j<matrix[i].length; j++){
        console.log(matrix[i][j]);
    }
}
```

#### 8、基本类型和引用类型

##### 基本类型：

number、boolean、string、undefined、null

基本类型变量，变量传值(var a=b)时会被单独分配内存地址并克隆相应值。

##### 引用类型：

array、object、function、regexp...

引用类型变量，变量传值时不会单独分配内存地址，而是让新变量指向同一内存地址。

基本类型进行相等判断时，会比较值是否相等。

引用类型进行相等判断时，会比较地址是否相等。

#### 9、浅克隆

浅克隆：只克隆数组的第一层，如果是多维数组，或者数组中的项是其他引用类型值，则不克隆其他层。

浅克隆：准备一个空的结果数组，然后使用for循环遍历原数组，将遍历到的项都推入结果数组

浅克隆只克隆数组的一层，如果数组是多维数组，则克隆的项会“藕断丝连”

```js
//  浅克隆案列
var arr1 = [1, 2, 3, 4];

// 结果数组
var result = [];

// 遍历原数组中的每一项，把遍历到的项推入到结果数组中
for (var i = 0; i < arr1.length; i++) {
	result.push(arr1[i]);
}

console.log(result); // [1, 2, 3, 4]
console.log(result == arr1);    // false，因为引用类型值进行比较的时候，等等比较的是内存地址
```

#### 10、总结：重要知识点

- 数组是什么？如何定义？
- 如何检查数组类型？
- 数组有那些常用方法？
- 数组的遍历相关算法、去重、随机样本和冒泡排序
- 基本类型值和引用类型值的区别

|            | 举例                                  | 当var a =b 变量传值时                        | 当用==比较时                               |
| ---------- | ------------------------------------- | -------------------------------------------- | ------------------------------------------ |
| 基本类型值 | 数字型、字符串型、布尔型、undefined型 | 内存中产生新的副本                           | 比较值是否相等                             |
| 引用类型值 | 对象、数组                            | 内存不产生新的副本，而是让新变量指向同一对象 | 比较内存地址是否相同，即比较是否时同一对象 |

## 第三部分、JS函数与DOM

### 一、函数

#### 1、函数

##### 1）函数的定义：

函数就是语句的封装，可以让这些代码方便地被复用

函数具有“一次定义，多次调用”的优点

必须先定义再使用

使用function关键字定义函数

```js
// function 定义函数的关键字
// funname 函数名，函数名必须复合JS标识符命名规则
// () 圆括号中是形参列表
// {} 大括号中是函数体语句
function funName(){
	// 函数体语句
}

// 函数表达式，将匿名函数赋值给一个变量
var fun = function () {
    // 函数体语句
}

// 调用函数，只需再函数名字后书写圆括号对即可
funName()
```

定义的函数是不会直接执行的

函数必须要被调用才会执行

函数可以提升，但函数表达式不能提升

##### 2）函数的参数

参数是函数内的一些待定值，在调用函数时，必须传入这些参数的具体值。

函数的参数可多可少，函数可以没有参数，也可以有多个参数，多个参数之间需要用逗号隔开

##### 3）函数的返回值

函数体内可以使用return关键字表示“函数的返回值”

调用一个有返回值得函数，可以被当做一个普通值，从而可以出现在任何可以书写值的地方

遇见returun即退出函数。

##### 4）数组的sort排序方法

数组的sort()的参数是函数

```js
var arr = [33,22,11,55];
// a,b分别是数组中靠前和靠后的项
arr.sort(function(a,b){
    return a-b
})
// 原型：从小到大排序
arr.sort(function(a,b){
    // 比较两项大于返回1，就交换位置，否则返回-1，就不交换。
    if (a>b){
        return 1;
    }else {
        return -1
    }
})
// 从大到小就是
arr.sort(function(a,b){
    return b-a
})
// 函数是JS中的一等公民，它可以当作参数传入另一个函数。
```

#### 2、函数拓展

#### 3、递归与克隆

##### 1）递归

函数的内部语句可以**调用这个函数自身**，从而发起对函数的**一次迭代**。在新的迭代中，又会执行调用函数自身的语句，从而又产生一次迭代。当函数执行到某一次时，不再进行新的迭代，函数被一层一层返回，函数被递归。

递归是一种较为**高级的编程技巧**，它把一个大型复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解。

用求数的阶乘来理解递归

4！=  4 * 3！ = 4 * 3  * 2!  = 4 * 3  * 2 * 1!

递归的要素

- 边界条件：确定递归到何时终止，也称为递归出口
- 递归模式：大问题是如何分解为小问题的，也称为递归体

```js
// 书写一个函数，这个函数内部自己会调用自己，从而形成递归。
function factorial(n) {
	// 函数的功能是计算n的阶乘，n!不就是n * (n-1)!么？？
	// 这个就是递归的出口，如果计算1的阶乘，可以不用递归了，直接告诉你答案就是1
	if (n == 1) return 1;
	// 如果询问的不是1的阶乘，就返回n * (n-1)!
	return n * factorial(n - 1);
}
var result = factorial(6);
alert(result);
```

```js
// 函数返回斐波那契数列中下标为n的那项的值
function Fibonacci(n){
	// 数列的下标为0的项和下标为1的项值是1，作为递归出口
	if (n == 0 || n == 1){
		return 1
	}
	// 斐波那契数列的本质特征就是每一项，都是前面两项的和
	return Fibonacci(n-1) + Fibonacci(n-2)
}
// 书写一个循环语句，获取斐波那契数列的前15项
for(var i = 0, arr = []; i<15; i++){
	arr.push(Fibonacci(i))
}
console.log(arr)
```

##### 2）深克隆

采用递归技术

使用递归思想，整体思路和浅克隆类似，但稍微进行一些改动

如果遍历到项是基本类型值，直接推入结果数组。

如果遍历到项是数组，则重复执行浅克隆的操作。

```js
// 原数组
var arr1 = [33, 44, 11, 22, [77, 88, [33, 44]]];

// 函数，这个函数会被递归
function deepClone(arr) {
	// 结果数组，“每一层”都有一个结果数组
	var result = [];
	// 遍历数组的每一项
	for (var i = 0; i < arr.length; i++) {
		// 类型判断，如果遍历到的项是数组
		if (Array.isArray(arr[i])) {
			// 递归
			result.push(deepClone(arr[i]));
		} else {
			// 如果遍历到的项不是数组，是基本类型值，就直接推入到结果数组中，
			// 相当于是递归的出口
			result.push(arr[i]);
		}
	}
	// 返回结果数组
	return result;
}
```

#### 4、作用域和闭包

##### 1）变量作用域

JavaScript是函数级作用域编程语言：变量只在其定义时所在的function内部有意义

**局部变量**：定义在函数内部的变量，作用域是函数内。

如果不将变量定义在任何函数的内部，此时这个变量就是**全局变量**，它在任何函数内都可以被访问和更改。

遮蔽效应

如果函数中也定义了和全局同名的变量，则函数内的变量会将全局的变量“遮蔽”。

形参也是局部变量

一个函数内部定义一个函数，和局部变量类似，定义在一个函数内部的函数是**局部函数**

作用域链

在函数嵌套中，变量会从内到外逐层寻找它的定义。

在初次给变量赋值时，如果没有加var，则将被定义为全局变量。

##### 2）闭包

JavaScript中函数会产生闭包(closure)。闭包是函数本身和该函数声明时所处的环境状态的组合。

函数能够“记忆住”其定义时所处的环境，即使函数不在其定义的环境中被调用，也能访问定义时所处环境的变量。

观察闭包现象

在JavaScript中，每次创建函数时都会创建闭包。

但是，闭包特性往往需要将函数“换一个地方”执行，才能被观察出来。

闭包很有用，因为它允许我们将数据与操作该数据的函数关联起来。这与“面向对象编程”有少许相似之处。

闭包的功能：记忆性、模拟私有变量。

###### 闭包的记忆性

当闭包产生时，函数所处环境的状态**会始终保持在内存中**，**不会在外层函数调用后被自动清除**。这就是闭包的**记忆性**。

```js
function createCheckTemp(standardTemp) {
	function checkTemp(n) {
		if (n <= standardTemp) {
			alert('你的体温正常');
		} else {
			alert('你的体温偏高');
		}
	}
    // 将内部函数传递出去
	return checkTemp;
}

// 创建一个checkTemp函数，它以37.1度为标准线
var checkTemp_A = createCheckTemp(37.1);
// 再创建一个checkTemp函数，它以37.3度为标准线
var checkTemp_B = createCheckTemp(37.3);

checkTemp_A(37.2);
checkTemp_A(37.0);
checkTemp_B(37.2);
checkTemp_B(37.0);
```

###### 闭包模拟私有变量

```js
// 封装一个函数，这个函数的功能就是私有化变量
function fun() {
	// 定义一个局部变量a
	var a = 0;

	return {
		getA: function () {
			return a;
		},
		add: function () {
			a++;
		},
		pow: function () {
			a *= 2;
		}
	};
}

var obj = fun();
// 如果想在fun函数外面使用变量a，唯一的方法就是调用getA()方法
console.log(obj.getA());
// 想让变量a进行加1操作
obj.add();
obj.add();
obj.add();
console.log(obj.getA());
obj.pow();
console.log(obj.getA());
```

###### 使用闭包的注意点：

不能滥用闭包，否则会造成网页的性能问题，严重时可能导致内存泄漏。所谓内存泄漏是指程序中已动态分配的内存由于某种原因未释放或无法释放。

##### 3） 立即调用函数表达式IIFE

IIFE（Immediately Invoked Function Expression）立即调用函数表达式是一种特殊的JavaScript函数写法，**一旦被定义，就立即被调用**。

函数必须转为“函数表达式”才能被调用。

已添加圆括号或+号或-号方式转化

常规使用圆括号

```js
// 利用IIFE给变量赋值
var age = 42;
var sex = '女';
var title = (function () {
	if (age < 18) {
		return '小朋友';
	} else {
		if (sex == '男') {
			return '先生';
		} else {
			return '女士';
		}
	}
})();
console.log(title)
```

```js
// IIFE功能2-将全局变量变为局部变量
var arr = [];
for (var i = 0; i < 5; i++) {
	(function(i){
		arr.push(function () {
			alert(i);
		});
	})(i);
}
arr[0]();
arr[1]();
arr[2]();
arr[3]();
arr[4]();
```

#### 5、总结：

##### 1）重点内容

- 什么是函数
- 函数的参数和返回值
- 函数的相关算法题

##### 2）难点内容

- 递归、递归算法题
- 作用域和闭包
- IIFE

### 二、DOM

DOM是JS操控HTML和CSS的桥梁

节点思维：把html的每个标签看做节点

DOM(Document Object Model,文档对象模型)是JavaScript操作Html文档的接口，使文档操作变得非常优雅、简便。

DOM最大的特点就是将文档表示为**节点树**。

#### 1、DOM基本概念

##### Document对象

访问元素节点主要依靠document对象，

document对象是DOM中最重要的东西，几乎所有**DOM的功能都封装在了document对象中**。

document对象野表示整个HTML文档，它是DOM节点树的根

document对象的nodeType属性值9

##### nodeType属性

node --节点，type--类型

##### 访问元素节点的常用方法

| 方法                              | 功能                   | 兼容性 |
| :-------------------------------- | :--------------------- | :----- |
| document.getElementById()         | 通过id得到元素         | IE6    |
| document.getElementsByTagName()   | 通过标签名得到元素数组 | IE6    |
| document.getElementsByClassName() | 通过类名得到元素数组   | IE9    |
| document.querySelector()          | 通过选择器得到元素     | IE9    |
| document.querySelectorAll()       | 通过选择器得到元素数组 | IE9    |

###### document.getElementById()

通过id获取元素

```html
<div id="box">
    我是一个盒子
</div>
<p id="para">
    一段话
</p>
<script>
    // 通过id获取元素节点
    var box = document.getElementById('box')
    var para = document.getElementById('para')
</script>
```

> 注意事项
>
> - 如果页面上有相同id的元素，则只能得到第一个
> - 不管元素藏的位置多深，都能通过id把它找到

###### document.getElementsByTagName()

通过标签名获取元素

```html
<div id="box1">
    <p>一段话</p>
    <p>一段话</p>
    <p>一段话</p>
    <p>一段话</p>
</div>
<div id="box2">
    <p>一段话</p>
    <p>一段话</p>
    <p>一段话</p>
    <p>一段话</p>
</div>
<script>
    // 获取全部的p标签
    var ps = box1.getElementsByTagName('p')
    // 只获取第一个box1的p标签
    var box1 = document.getElementById('box1')
    var bpx1_ps = box1.getElementsByTagName('p')
</script>
```

> 注意事项：
>
> - 数组方便遍历，从而可以批量操控元素节点
> - 即使页面只有一个指定标签名的节点，也将得到长度为1的数组
> - 任何一个节点元素也可以调用document.getElementsByTagName()方法，从而得到其内部的某种类的元素节点

###### document.getElementsByClassName()

通过类名获取元素

```html
<div class="spec">盒子</div>
<div class="xxx">盒子</div>
<div class="spec">盒子</div>
<div class="spec">盒子</div>
<script>
    var spec = document.getElementByClassName('spec')
</script>
```

> 注意事项：
>
> - 某个节点元素也可以调用getElementsByClassName()方法，从而得到其内部的某类名的元素节点

###### querySelector()

通过选择器获取元素

```html
<div id="box1">
    <p>第一段话</p>
    <p class="spec">第二段话</p>
    <p>第三段话</p>
</div>
<script>
    var the_ = document.querySelector('#box1.spen');
</script>
```

> 注意事项：
>
> - querySelector()方法只能得到页面上一个元素，如果有多个元素符合条件，则只能得到第一个元素

###### querySelectorAll()

- querySelectorAll()方法的功能是通过选择器得到元素数组
- 即使页面上只有一个符合选择器的节点，也将得到长度为1的数组

```html
<div>
    <ul id="list1">
        <li>001</li>
        <li>002</li>
        <li>003</li>
    </ul>
    <ul id="list2">
        <li>001</li>
        <li>002</li>
        <li>003</li>
    </ul>
</div>
<script>
    var list = document.querySelectorAll('#list2 li')
</script>
```

##### 节点关系

父节点(parenNode)、子节点(childNodes)、

|      关系      | 考虑所有节点    | 只考虑元素节点         |
| :------------: | --------------- | ---------------------- |
|     子节点     | childNodes      | children               |
|     父节点     | parentNode      | 同                     |
|  第一个子节点  | firstChild      | firstElementChild      |
| 最后一个子节点 | lastChilde      | lastElementChild       |
| 前一个兄弟节点 | previousSibling | previousElementSibling |
| 后一个兄弟节点 | nextSibling     | netElementSibling      |

> 注意：
>
> - 在DOM，文本节点也属于节点，在使用节点的关系时一定要注意。
> - 在标准的W3C规范中，空白文本节点也算节点

##### 书写节点关系函数

###### 寻找所有元素子节点函数

###### 寻找前一个元素兄弟节点

###### 获得某元素的所有的兄弟节点

```html
<div id="box">
	<p>我是段落</p>
	<p>我是段落</p>
	<p>我是段落</p>
	<p id="fpara">我是段落fpara</p>
	我是文本
	<!-- 我是注释 -->
	<p id="para">
		我是段落para
		<span>1</span>
		<span>2</span>
		<span>3</span>
	</p>
	<p>我是段落</p>
	<p>我是段落</p>
	<p>我是段落</p>
</div>

<script>
	var box = document.getElementById('box');
	var para = document.getElementById('para');
	var fpara = document.getElementById('fpara');

	// 封装一个函数，这个函数可以返回元素的所有子元素节点（兼容到IE6），类似children的功能
	function getChildren(node) {
		// 结果数组
		var children = [];
		// 遍历node这个节点的所有子节点，判断每一个子节点的nodeType属性是不是1
		// 如果是1，就推入结果数组
		for (var i = 0; i < node.childNodes.length; i++) {
			if (node.childNodes[i].nodeType == 1) {
				children.push(node.childNodes[i]);
			}
		}
		return children;
	}

	console.log(getChildren(box));
	console.log(getChildren(para));

	// 封装一个函数，这个函数可以返回元素的前一个元素兄弟节点（兼容到IE6），类似previousElementSibling的功能
	function getElementPrevSibling(node) {
		var o = node;
		// 使用while语句
		while (o.previousSibling != null) {
			if (o.previousSibling.nodeType == 1) {
				// 结束循环，找到了
				return o.previousSibling;
			}

			// 让o成为它的前一个节点，就有点“递归”的感觉
			o = o.previousSibling;
		}
		return null;
	}

	console.log(getElementPrevSibling(para));
	console.log(getElementPrevSibling(fpara));

	// 封装第三个函数，这个函数可以返回元素的所有元素兄弟节点
	function getAllElementSibling(node) {
		// 前面的元素兄弟节点
		var prevs = [];
		// 后面的元素兄弟节点
		var nexts = [];
		
		var o = node;
		// 遍历node的前面的节点
		while(o.previousSibling != null) {
			if(o.previousSibling.nodeType == 1){
				prevs.unshift(o.previousSibling);
			}
			o = o.previousSibling;
		}

		o = node;

		// 遍历node的后面的节点
		while(o.nextSibling != null) {
			if(o.nextSibling.nodeType == 1){
				nexts.push(o.nextSibling);
			}
			o = o.nextSibling;
		}

		// 将两个数组进行合并，然后返回
		return prevs.concat(nexts);
	}

	console.log(getAllElementSibling(para));
```

#### 2、节点操作

##### 创建节点

document.createElemnet()方法用于创建一个指定标签名(tag name)的html元素

```js
var oDiv = document.createElemnet('div')
```

注意：

新创建的节点是“孤儿节点“，这意味着它并没有被挂载到DOM树上，我们无法看见它

##### 挂载节点

使用appendChild()或insertBefores()方法将孤儿节点插入到DOM树上。

###### appendChild()

任何已经在DOM树上的节点，都可以调用appendChild()方法，它可以将孤儿节点挂载到它的内部，成为它的最后一个子节点。

```js
父节点.appendChild(孤儿节点)
```

###### insertBefores()

任何已经在DOM树上的节点，都可以调用insertBefore()方法，它可以将孤儿节点挂载到它的内部，成为它的"标杆子节点"之前的节点。

```js
父节点.insertBefore(孤儿节点, 标杆节点)
```

##### 移动节点

如果将已经挂载到DOM树上的节点成为appendChild()或insertBefores()的参数，这个节点将会被移动。

```js
新父节点.appendChild(已经有父亲的节点)
新父节点.insertBefore(已经有父亲的节点, 标杆节点)
```

这意味着一个节点不能同时位于DOM树的两个位置

##### 删除节点

removeChild()方法从DOM中删除一个子节点

```js
父节点.removeChild(要删除子节点);
```

节点不能主动删除自己，必须由父节点删除它。

##### 克隆节点

cloneNode()方法可以克隆节点，克隆出的节点是”孤儿节点“。

```js
var 孤儿节点 = 老节点.cloneNode();
var 孤儿节点 = 老节点.cloneNode(true);
// 参数是一个布尔值，表示是否采用深度克隆：如果为true,则该节点的所有后代节点都被克隆，如果为false，则只克隆该节点本身。默认是false
```

##### 设置改变元素节点中的内容

改变元素节点中的内容可以使用两个相关属性：

###### innerHTML()

innerHTML属性能以HTML语法设置节点的内容

```html
<div id="box"></div>
<script>
    var oBox = document.getElementById('box')
    oBox.innetHTML = '<ul><li>苹果</li><li>橙子</li></ul>'
</script>
```

###### innerText()

innerText属性只能以纯文本的形式设置节点的内容

```html
<div id="box"></div>
<script>
    var oBox = document.getElementById('box')
    oBox.innetText = '坚持很辛苦~坚持就是胜利！！！'
</script>
```

##### 改变节点样式

```javascript
oBox.style.backgroundColor = 'red';
oBox.style.backgroundImage = 'url(images/001.jpg)';
oBox.style.fontSize = '32px';
```

#### 延迟运行

```js
window.onload = function(){
	...
}
```

#### 3、DOM事件

##### 事件监听

什么是事件：用户与网页的交互动作

- 当用户点击元素
- 当鼠标移动到元素上时
- 当文本框的内容被改变时
- 当键盘在文本框中被按下时
- 当网页已加载完毕时
- ......

监听：顾名思义，就是让计算机随时能够发现这个事件发生了，从而执行程序员预先编写的一些程序。

设置事件监听的方法主要由onxxx和addEventListener()两种方法

###### onXXX的方法：

```js
oBox.onclick = function(){
	// 点击盒子时，执行语句
}
```

###### 常见的鼠标事件监听

| 事件名       | 事件描述                                  |
| :----------- | :---------------------------------------- |
| onclick      | 当鼠标单击某个对象                        |
| ondblclick   | 当鼠标双击某个对象                        |
| onmousedown  | 当某个鼠标按建在某个对象上被按下          |
| onmouseup    | 当某个鼠标按建在某个对象上被松开          |
| onmousemove  | 当某个鼠标按建在某个对象上被移动          |
| onmouseenter | 当鼠标进入某个对象（相似事件onmouseover） |
| onmouseleave | 当鼠标离开某个对象（相似事件onmouseout）  |

###### 常见的键盘事件监听

| 事件名     | 事件描述                                                     |
| ---------- | ------------------------------------------------------------ |
| onkeypress | 当某个键盘的键被按下（系统按钮如箭头键和功能键无法得到识别） |
| onkeydown  | 当某个键盘的键被按下（系统按钮可以识别，并且会先于onkeypress发生） |
| onkeyup    | 当某个键盘的键被松开                                         |

###### 常见的表单事件监听

| 事件名   | 事件描述                                |
| -------- | --------------------------------------- |
| onchange | 当用户改变域的内容                      |
| onfocus  | 当某元素获得焦点（比如tab键或鼠标点击） |
| onblur   | 当某元素失去焦点                        |
| onsubmit | 当表单被提交                            |
| onreset  | 当表单被重置                            |

常见的页面事件监听

| 事件名   | 事件描述               |
| -------- | ---------------------- |
| onload   | 当页面或图像被完成加载 |
| onunload | 当用户退出页面         |

##### 事件传播

当盒子嵌套时事件监听的执行顺序？

事件的传播是：先从外到内，然后再从内到外。

**捕获阶段**（capturing phase）-- 从外到内

**冒泡阶段**（Bubbling phase）-- 从内到外

onxxx这样的写法**只能监听冒泡阶段**

```js
// DOM0级事件监听：只能监听冒泡阶段
oBox.onclick = function () {
	......
};
```

###### addEventListener()方法

```js
// DOM2级事件监听
oBox.addEventListener('click', function(){
    ......
}, true);
// 第三个参数：true 监听捕获阶段，false监听冒泡阶段
```

> 注意事项：
>
> - 最**内部元素不再区分捕获或冒泡阶段**，会先执行写在前面的监听，然后执行后写的监听
> - 如果给元素设置相同的两个或多个同名事件，则DOM0级写法**后面写的会覆盖先写的；而DOM2级会按顺序执行**

##### 事件对象

- 事件处理函数提供一个形式参数，它是一个对象，**封装了本次事件的细节**
- 这个参数通常用**单词event或字母e**来表示

```js
oBox.onmousemove = function (e) {
    // 对象e就是这次事件的“事件对象”
}
```

###### 鼠标位置

|属性|属性描述|
|-|-|
|clientX|鼠标指针相对于浏览器的水平坐标|
|clientY|鼠标指针相对于浏览器的垂直坐标|
|pageX|鼠标指针相对于整张网页的水平坐标|
|pageY|鼠标指针相对于整张网页的垂直坐标|
|offsetX|鼠标指针相对于事件源元素的水平坐标|
|offsetY|鼠标指针相对于事件源元素的垂直坐标|

> 鼠标滚轮事件是onmousewheel，它的事件对象e提供deltaY属性表示鼠标滚动方向，向下滚动时返回正值，向上滚动时返回负值。



###### e.charCode和e.keyCode

- e.charCode属性通常用于onkeypress事件中，表示用户输入的字符的“字符码”
- e.keyCode属性通常用于onkeydown事件和onkeyup中，表示用户按下的键的“键码”

###### charCode字符码

| 字符        | 字符码 |
| ----------- | ------ |
| 数字0~数字9 | 48~57  |
| 大写字母A~Z | 65~90  |
| 小写字母a~z | 97~122 |

###### keyCode键码

| 按建            | 键码                                                         |
| --------------- | ------------------------------------------------------------ |
| 数字0~数字9     | 48~57(同charCode键码完全相同)                                |
| 字母不分大小a~z | 65~90(同cahrCode键码的大写字母A~Z，而keyCode不分大小写，一律为65~90) |
| 四个方向键      | 37、38、39、40                                               |
| 回车键          | 13                                                           |
| 空格键          | 32                                                           |

###### e.preventDefault()方法

- e.preventDefault()方法用来阻止事件产生的“默认动作 ”
- 一些特殊的业务需求，需要阻止事件的“默认动作”

```html
<div>
	<input type="text" id="myInput" placeholder="只能输入数字和小写字母">
</div>
<script>
	// 获取输入框对象
	var myInput = document.getElementById('myInput')
	// 监听键盘输入事件
	myInput.onkeypress = function (e) {
		// 如果不是数字和小写字母的区间
		if ( !(e.charCode>=48 && e.charCode <=57 ||  e.charCode>=97 && e.charCode <=122) ){
			// 阻止默认事件
			e.preventDefault()
		}
	}
</script>
```

###### e.stopPropagation()方法

e.stopPropagation()方法用来阻止事件继续传播

在一些场合，非常有必要切断事件继续传播，否则会造成页面特效显示bug

主要用于阻止嵌套盒子的捕获阶段和冒泡阶段的事件传播

##### 事件委托

在说明事件委托前了解两个问题

###### 批量添加事件监听

```html
<div>
	<ui id="list01">
		<li>列表名</li>
		<li>列表名</li>
		<li>列表名</li>
	</ui>
</div>
<script>
	// 获取相应节点元素
	var oList = document.getElementById('list01')
	var oLi = document.getElementsByTagName('li')
	// 遍历节点的元素
	for (i=0; i<=oLi.length; i++) {
		// 监听每个节点元素的鼠标点击事件
		oLi[i].onclick = function () {
			// this 代表当前点击元素
			// 设置当前点击元素的颜色属性
			this.style.color = 'red'
		}
	}
</script>
```

> 批量事件监听的性能问题
>
> - 每个事件监听注册都会消耗一定的系统内存，数量太大，内存消耗会非常大
> - 每个元素的事件处理函数都是不同的函数，这些函数本身会占用内存

###### 新增元素动态绑定事件

```html
<div>
	<button id="btn">点我添加列表项</button>
	<ul id="list"></ul>
</div>
<script>
	// 获取元素节点
	oBtn = document.getElementById('btn');
	oList = document.getElementById('list');
	// 按钮事件添加列表项元素
	oBtn.onclick = function(){
		// 创建一个孤岛节点元素
		var oLi = document.createElement('li')
		oLi.innerHTML = '列表项'
		// 挂载到dom树
		oList.appendChild(oLi)
		// 添加事件监听
		oLi.onclick = function () {
			this.style.color = 'red'
		}
	}
</script>
```

> 新增动态绑定事件也是占内存的，内存消耗大
>
> 大量事件监听、大量事件处理函数都会产生大量消耗内存

###### 事件委托

利用事件冒泡机制，将后代元素事件委托给祖先元素

事件委托通常需要结合使用e.target属性

| 属性          | 属性描述                             |
| ------------- | ------------------------------------ |
| target        | 触发此事件的最早元素，即“事件源元素” |
| currentTarget | 事件处理程序附加到的元素             |

```html
<div>
	<button id="btn">点我添加列表项</button>
	<ul id="list"></ul>
</div>
<script>
	// 获取节点元素
	var oBtn = document.getElementById('btn');
	var oList = document.getElementById('list');
	// 事件委托，将后代元素事件挂载到祖先元素身上
	oList.onclick = function(e){
		// 通过e.target属性，获取事件源元素，设置颜色样式值
		e.target.style.color = 'red';
	}
	// 按钮添加元素事件
	oBtn.onclick = function(){
		// 创建孤岛元素
		var oLi = document.createElement('li');
		oLi.innerHTML = '列表项';
		// 挂载上树
		oList.appendChild(oLi);
	}
</script>
```

> 通过事件委托，减少了事件监听的数量，解决了性能问题
>
> 使用事件委托要注意：不能委托不冒泡的事件给祖先元素
>
> 最内层元素不能再有额外的内层元素

##### 4、定时器：setInterval()

- setInterval()函数可以重复调用一个函数，在每次调用之间具有固定的时间间隔


```js
setInterval(function(){
    // 被重复调用的函数代码
}, 2000);
// 第一个参数是函数
// 第二个参数是间隔，以毫秒为单位，1000毫秒=1秒
```

- setInterval()函数可以接收第3、4.....个参数，它们将按顺序传入函数

```js
setInterval(function(a, b){
    // 形参a的值为88，形参b的值为66
}, 2000, 88, 66);
```

- 具名函数也可以传入setInterval()

```js
var a = 0;
function funName(){
    console.log(++a);
}
setInterval(funName, 1000);
// 具名函数当作第一参数，注意不能写圆括号
```

- clearInterval()函数可以清除一个定时器

```js
// 设置定时器，并用timer变量接受这个定时器
var timer = setInterval(function(){
    
}, 2000);
// 点击按钮时，清除定时器
oBtn.onclick = function (){
    clearInterval(timer);
}
```

- 定时器有叠加效果，为了防止定时器叠加，应该在设置定时器之前先清除定时器

```js
<script>
	// 获取元素
	var info = document.getElementById('info');
	var btnStart = document.getElementById('btnStart');
	var btnEnd = document.getElementById('btnEnd');
	var a = 0;
	var timer;  // 定时器的全局变量名
	// 开始按钮监听
	btnStart.onclick = function(){
		// 为了防止定时器叠加，在设置定时器前应设置清除定时器
		clearInterval(timer);
		// 设置定时器
		timer = setInterval(function(){
			info.innerText = ++a;
		},1000);
	}
	// 结束按钮监听
	btnEnd.onclick = function(){
		clearInterval(timer);
	}
</script>
```

##### 延时器setTimeout()

setTimeout()函数设置一个延时器，当指定时间到了之后，会执行函数一次，不再重复执行。

```js
setTimeout(function(){
    // 这个函数会在2秒后执行一次
}, 2000);
// 第一个参数是函数
// 第二个参数是延后时间，单位毫秒
```

清除延时器

clearTimeout()函数清除延时器

```js
var timer;
timer = setTimeout(function(){
    alert('两秒后显示');
}, 2000)
// 点击取消延时器
btn.onclick = function(){
    clearTimeout(timer);
}
```

##### 初识异步语句

- setInterval()和setTimeout()就是两个异步语句
- **异步(asynchronous)**：**不会阻塞CPU继续执行其他语句，当异步完成时，会执行“回调函数”(callback)**

##### 5、使用定时器实现动画

利用的就是“视觉暂留”原理

使用定时器实现动画较为不便：

- 不方便根据动画总时间计算步长
- 运动方向要设置正负
- 多运动进行叠加较为困难

##### JS和CSS3结合实现动画

- CSS3的transition过度属性可以实现动画
- JavaScript可以利用CSS3的transition属性轻松实现元素动画
- JS和CSS3结合实现动画规避了定时器制作动画的缺点

```html
<style>
	#box{
		width: 100px;
		height: 100px;
		background-color: orange;
		position: absolute;
		top: 100px;
		left: 100px;
	}
</style>
<button id="btn">点我开始移动</button>
<div id="box"></div>
<script>
	// 获取元素
	var oBtn = document.getElementById('btn');
	var oBox = document.getElementById('box');
    // 标识量
    var pos = 1;  // 1左边，2右边
	// 点击事件监听
	oBtn.onclick = function(){
		// 增加动画效果，在移动语句前面加上CSS的过度属性
		oBox.style.transition = 'all 2s linear 0s';
        if(pos ==1){
            // 向右移动盒子
            oBox.style.left = '1100px';
            pos = 2;
        }else if(pos ==2){
            // 向左移动盒子
            oBox.style.left = '100px';
            pos = 1;
        }
	}
</script>
```

##### 函数节流

函数节流：一个函数执行一次后，只有大于设定的执行周期后才允许执行第二次。

函数节流非常容易实现，只需要借助setTimeout()延时器

```js
// 函数节流公式
var lock = true;
function 需要节流的函数(){
    // 如果锁时关闭状态，则不执行
    if(!lock)return;
    // 函数核心语句
    
    // 关锁
    lock = false;
    
    // 指定毫秒数后将锁打开
    setTimeout(function(){
        lock = true
    },2000);
}
```

### 三、BOM

#### BOM是什么

BOM（Browser Object Model，浏览器对象模型）是JS与浏览器窗口交互的接口

一些与浏览器改变尺寸、滚动条滚动相关的特效，都要借助BOM技术

##### window对象

window对象是**当前JS脚本运行所处的窗口**，而这个窗口中包含DOM结构，**window.document属性就是document对象**

在有标签页功能的浏览器中，每个标签都拥有自己的window对象；也就是说，同一个窗口的标签页之间不会共享一个window对象

##### 全局变量是window的属性

```js
var a = 10;
console.log(window.a == a);  // true
```

这就意味着，**多个 js文件之间是共享全局作用域的**，即js文件没有作用域隔离功能

##### 内置函数普遍是window的方法

如setInterval()、alert()等内置函数，普遍是window的方法

```js
console.log(window.alert == alert);  // true
console.log(window.setInterval == setInterval);  // true
```

##### 窗口尺寸相关属性

| 属性        | 意义                                                     |
| ----------- | -------------------------------------------------------- |
| innerHeight | 浏览器窗口的内容区域的高度，包含水平移动条（如果有的话） |
| innerWidth  | 浏览器窗口的内容区域的宽度，包含垂直移动条（如果有的话） |
| outerHeight | 浏览器窗口的外部高度                                     |
| outerWidth  | 浏览器窗口的外部宽度                                     |

> 获得不包含滚动条的窗口宽度，要用**document.documentElement.clientWidth**

##### resize事件

在窗口大小改变之后，就会触发resize事件，可以使用window.onresize或者window.addEventListener('resize')来绑定事件处理函数

```js
// 监听浏览器窗口改变尺寸事件
window.onresize = function(){
    var root = document.documentElement;
    console.log('窗口改变尺寸了', root.clientWidth, root.clientHeight)
}
```

##### 窗口卷动高度

window.scrollY属性标识在垂直方法已滚动的像素值

document.documentElement.scrollTop属性也表示窗口卷动高度

```js
// 返回页面开始的特效
document.documentElement.scrollTop = 0;
```

###### 返回顶部按钮制作

返回顶部的原理：改变document.documentElement.scrollTop属性，通过定时器逐步改变此值，则将用动画形式返回顶部

```html
<head>
    <style>
        body {
            height: 5000px;
            /* 设置背景图片，线性渐变：到底，蓝色->绿色->红色 */
            background-image: linear-gradient(to bottom, blue, green, red);
        }
        .backtotop{
            width: 50px;
            height: 50px;
            background-color: rgba(255, 255, 255, .6);
            position: fixed; /* 定位方式：固定定位--相对浏览器窗口定位 */
            bottom: 100px;
            right: 100px;
            cursor: pointer;  /* 鼠标变成小手状 */
        }
    </style>
</head>
<body>
    <div class="backtotop" id="backtotopBtn">返回顶部</div>

    <script>
        var backtotopBtn = document.getElementById('backtotopBtn');
        var timer;
        backtotopBtn.onclick = function() {
            // 设表先关
            clearInterval(timer);
            // 设置定时器
            timer = setInterval(function(){
                // 不断让scrollTop减少
                document.documentElement.scrollTop -= 10;
                // 定时器关闭条件 
                if(document.documentElement.scrollTop <= 0){
                    clearInterval(timer);
                }
            }, 20)
        }
    </script>
</body>
```

##### scroll事件

在窗口被卷动后，就会触发scroll事件，可以使用window.onscroll或者window.addEventListener('scroll')来绑定事件处理函数

##### Navigator对象

window.navigator属性可以检索navigator对象，它内部含有用户此次活动的**浏览器的相关属性和标识**

| 属性       | 意义                                         |
| ---------- | -------------------------------------------- |
| appName    | 浏览器官方名称                               |
| appVersion | 浏览器版本                                   |
| userAgent  | 浏览器的用户代理（含有内核信息和封装壳信息） |
| platform   | 用户操作系统                                 |

##### History对象

window.history对象提供了操作浏览器会话历史的接口

常用操作就是模拟浏览器回退按钮

```js
history.back();  // 等同于点击浏览器的回退按钮
history.go(-1);  // 等同于history.back()
```

##### Location对象

window.location标识当前所在网址，可以通过给这个属性赋值命令浏览器精细页面跳转

```js
windows.location = 'http://baidu.com';
windows.location.href = 'http://baidu.com';
```

###### 重新加载当前页面

可以调用location的reloak方法以重新加载当前页面，参数true表示强制从服务器强制加载

```js
window.location.reload(true);
```

###### get请求查询参数

window.location.search属性即为当前浏览器的GET请求查询参数

##### offsetTop属性

offsetTop属性，表示此元素到定位祖先元素的垂直距离

定位祖先元素：在祖先中，离自己最近的且拥有定位属性的元素

如果没有定位属性的祖先元素则表示元素到浏览器窗口顶端的垂直距离

##### 楼层导航小效果

## 第四部分、面向对象

### 一、对象

#### 认识对象

对象(object)是“键值对”的集合，表示属性和值的映射关系

```js
var obj = {key:value, key:value, key:value, ...}
```

##### 属性的访问

- 可以用“**点语法**”访问对象中指定键的值

  ```js
  obj.name;
  ```

- 如果属性名不符合js标识符命名规范，则必须用**方括号的写法**访问

  ```js
  obj.['first-name'];
  ```

- 如果属性名以变量形式存储，则必须使用方括号形式

- 如果事先属性的名称未知或者调用的属性是动态变化的就不能用点语法，使用方括号法可以最大程度提升对象调用属性的灵活度

##### 属性的修改

直接使用赋值运算符重新对某属性赋值即可更改属性值

##### 属性的创建

如果没有对象本身没有某个属性值，则用点语法赋值时，这个属性会被创建出来

##### 属性的删除

如果要删除某个对象的属性，采用delete操作符

```js
var obj = {a:1, b:6};
delete obj.a;
```

#### 对象的方法

##### 什么是方法：

如果某个属性值是函数，则它也被称为对象的“方法”。

##### 方法的调用

使用“点语法”可以调用对象的方法

```js
obj.funName();
```

方法也是函数，只不过方法是对象的“函数属性”，它需要用对象打点调用

```js
var xiaoqiang = {
    name: '小强',
    sex: '男',
    age: 14,
    sayHello: function() {
        console.log('你好!我是小强，我14岁了，是个男生！');
    }
}
xiaoqiang.sayHello();
```

#### 对象的遍历

- 和遍历数组类似，对象也可以被遍历，遍历对象需要使用for...in...循环
- 使用for...in...循环可以遍历对象的每个键
- 在ES6中还有一些新的遍历方式

##### for...in...循环

```js
for(var k in obj){
    conlog.log('属性' + k + '的值是' + obj[k])
}
```

#### 对象的深浅克隆

- 对象是引用类型值，这就意味着：
  - 不能使用var obj2 =obj1这样的语法克隆一个对象
  - 使用==或者===进行对象比较，比较的是它们是否内存中的同一地址指向，而不是比较值是否相同 

 ##### 浅克隆

- **浅克隆：只克隆对象的“表层”**，如果对象的某些属性值是引用类型值，则不进一步克隆，只传递它们的引用

- 使用for...in...循环即可实现对象的浅克隆

  

##### 深克隆

- 深克隆：克隆对象的全貌，不论对象的属性值是否引用类型，都将它们实现克隆
- 和数组的深克隆类似，对象的深克隆采用递归方法

```js
function deepClone(o){
    // 传入参数是数组还是对象
    if(Array.isArray(0)){
        // 数组
        var result = [];
        for(var i = 0; i<=o.length; i++){
            result.push(deepclone(o[i]));
        }
    }else if(typeof o == 'object'){
        // 对象
        var result = {};
        for(var k in o){
            result[k] = deepClone(o[k]);
        }
    }else {
        // 基本类型
        var result = o;
    }
    return result;
}
```

### 二、上下文规则

#### 认识上下文

睡觉前刷牙，这是好习惯

函数的上下文：

- 函数中可以使用this关键字，它表示函数的上下文

- 与中文中“这”函数中的this具体指代什么必须通过调用函数时的“前言后语”来判断

```js
var xiaoqiang = {
    name: '小强',
    sex: '男',
    age: 14,
    sayHello: function() {
        console.log('你好!我是' + this.name + '，我' + this.age + '岁了，是个' + this.sex + '生！');
    }
}
xiaoqiang.sayHello();  // '你好!我是小强，我14岁了，是个男生！'

var sayHello = xiaoqiang.sayHello;
sayHello();  //  '你好!我是undefined，我undefined岁了，是个undefined生！'
```

- 同一个函数，用不同的形式调用它，则函数的上下文不同

  - 情形1：对象打点调用函数，函数中的this指代这个打点的对象

    ```js
    xiaoqiang.sayHello()
    ```

  - 情形2：圆括号直接调用函数，函数中的this指代window对象

    ```js
    var sayHello = xiaoqiang.sayHello;
    sayHello();
    ```

- 函数的上下文由调用形式决定的

#### 上下文规则

- 函数的上下文(this关键字)由调用函数的方式决定，function是“运行时上下文”策略

- 函数不调用，则不能确定函数的上下文

##### 规则：

- 规则1：对象打点调用它的方法函数，则函数的上下文是这个打点的对象

  - 对象.方法()

    ```js
    var obj1 = {
        a: 1,
        b: 2,
        fn:function(){
            console.log(this.a + this.b);
        }
    }
    var obj2 = {
        a: 66,
        b: 33,
        fn: obj1.fn
    }
    obj2.fn(); // 构成对象.方法()的形式，适用规则2，this是打点对象
    ```

    

- 规则2：圆括号直接调用函数，则函数的上下文是window对象

  - 函数()

    ```js
    var obj1 = {
        a: 1,
        b: 2,
        fn:function(){
            console.log(this.a + this.b);
        }
    }
    var a = 3;
    var b = 4;
    var fn = obj1.fn;
    fn(); // 构成函数()的形式，适用规则2，this 是window对象
    ```

- 规则3：数组(类数组对象)枚举出函数进行调用，上下文是这个数组(类数组对象)

  - 数组[下标]（）

    ```js
    // 例题1
    var arr = ['A', 'B', 'C'， function(){
        console.log(this[0]);
    }]
    arr[3]();  // 构成数组[下标]()的形式，上下文是这个类数组对象
    // 例题2
    function fun() {
        arguments[3]();  // 构成数组[下标]()的形式，上下文是这个类数组对象
    }
    fun('A', 'B', 'C'， function(){
        console.log(this[1]);
    })
    ```

- 规则4：IIFE中的函数，上下文是window对象

  ```js
  var a = 1;
  var obj = {
      a: 2,
      fun: (function(){
          // IIFE函数立即执行带圆括号，this表示window对象
          var a = this.a;  
          return function(){
              console.log(a + this.a)  // a闭包的值为1，this.a值为2
          }
      })()  // 适用规则4,在IIFE的函数后圆括号，this表示window对象 
  };
  obj.fun();  // 适用规则1，对象.方法()，this表示打点对象
  // 运行结果是：3
  ```

- 规则5：定时器、延时器调用函数，上下文是window对象

  - setInterval(函数，时间);

  - setTimeout(函数，时间);

    ```js
    var obj = {
        a: 1,
        b: 2,
        fun: function(){
            console.log(this.a + this.b)
        }
    }
    var a = 3;
    var b = 4;
    setTimeout(obj.fun, 2000);  // 适用规则5，this=window对象
    // 结果是： 7
    
    setTimeout(function(){
        obj.fun();
    }, 2000); // 适用规则1，this=打点对象
    // 结果是： 3
    ```

- 规则6：事件处理函数的上下文是绑定事件的DOM元素

  - DOM元素.onclick = function(){};

    ```js
    function setColorToRed() {
        this.style.backgroundColor = 'red';
    }
    var box1 = document.getElementById('box1')
    var box2 = document.getElementById('box2')
    box1.onclick = setColorToRed;
    box2.onclick = setColorToRed;
    // 那个事件运行，this表示那个事件的元素
    ```


#### call和apply 指定上下文

##### 书写语法：

- 函数.call(上下文)
- 函数.apply(上下文)

```js
function sum(){
    alert(this.c + this.m + this.e);
};
var xiaoqiang = {
    c: 100，
    m: 80,
    e: 90
};
sum.call(xiaoqiang);  // 运行结果是：270
sum.apply(xiaoqiang);  // 运行结果是：270
```

##### call和apply的区别

```js
// 当函数带附加参数时才有区别 
function sum(x, y){
    alert(this.c + this.m + this.e + x + y);
};
var xiaoqiang = {
    c: 100，
    m: 80,
    e: 90
};
sum.call(xiaoqiang, 3, 5);  // call要用逗号罗列参数
sum.apply(xiaoqiang, [3, 5]);  // apply要把参数写到数组中
```

#### 上下文规则总结

| 规则            | 上下文           |
| --------------- | ---------------- |
| 对象.函数()     | 对象             |
| 函数()          | window           |
| 数组[下标]（）  | 数组             |
| IIFE            | window           |
| 定时器          | window           |
| DOM事件处理函数 | 绑定DOM的元素    |
| call和apply     | 任意指定         |
| 用new调用函数   | 秘密创建出的对象 |

### 三、构造函数与类

#### 用new操作符调用函数

新的函数调用方式：new 函数()

JS规定，使用new操作符调用函数会进行"四步走"

1. 函数体内会自动创建出一个空白对象
2. 函数的上下文（this）会指向这个对象
3. 函数体内的语句会执行
4. 函数会自动返回上下对象，即使函数没有return语句

```js
// 四步走详解：
function fun(){  // 1、被new的同时会创建一个空白的对象{}
    this.a = 3;  // 2、这时this的上下文指向这个空白对象this={}
    this.b = 5;  // 3、自动执行函数体内语句得到-->{a:3, b:5}
}                // 4、自动返回得到的对象-->{a:3, b:5}
var obj = new fun();
console.log(obj)
```

#### 类与实例

构造函数(视作为类)  --> new方法（实例化） --> 类的实例对象

类好比是“蓝图”：如同“蓝图”一样，类只描述对象会拥有哪些属性和方法、但是并不具体指明属性的值。

实例就是具体的对象

- “狗”是类，“史努比”、“小白”是实例
- “拉布拉多犬”也是类，是“狗”类的子类，具体到那只狗是实例

Java、C++等是“**面向对象**”（object-oriented）语言 -- 简称OO

面向对象”（object-oriented）语言 ：大概来说所谓的面向对象语言，就是描述刻画很多的类，然后这些类实例去进行配合工作来完成业务需求。这样开发语言我们就称为面向对象语言

JavaScript是“**基于对象**”（object-based）语言 -- 简称OB

JavaScript中的**构造函数可以类比于OO语言中的“类”**，写法的确类似，**但和真正OO语言还是由本质不同**。

我们在这里用**构造函数来充当类的概念和作用**

### 四、原型&&原型链

#### prototype

- 任何函数都有prototype属性，prototype是英语“原型”的意思

- prototype属性值是个对象，它默认**拥有constructor属性指向函数**

  ```js
  function sum(a, b){
      return a + b;
  }
  console.log(sum.prototype);  // {constructor: f}
  console.log(typeof sum.prototype);  // object
  console.log(sum.prototype.constructor === sum);  // true
  ```

- 普通函数来说的prototype属性没有任何用处，而**构造函数的prototype属性非常有用**

- **构造函数的prototype属性是它的实例的原型**



![image-构造函数与实例](\Assets\构造函数与实例.png)

#### 原型链查找

- JavaScript规定：**实例可以打点访问它的原型的属性和方法**，这被称为“原型链查找”

  ```js
  function People(name, age, sex){
      this.name = name;
      this.age = age;
      this.sex = sex;
  }
  // 在构造函数的prototype上添加nationality属性
  People.prototype.nationality = "china";
  var xiaoqiang = new People('小强', 12, '男');
  console.log(xiaoqiang.nationality);  // china
  // 实例可以打点访问原型的属性和方法
  // xiaoqiang本身是没有nationality，是访问它的原型获得
  ```

- 如果实例本身是具备与原型相同名的属性，则会原型链产生遮蔽，访问自身属性

#### hasOwnProperty

- hasOwnProperty方法可以检查对象是否真正“自已拥有某属性或者方法”

  ```js
  console.log(xiaoqiang.hasOwnProperty('name'));  // true
  console.log(xiaoqiang.hasOwnProperty('age'));  // true
  console.log(xiaoqiang.hasOwnProperty('nationality'));  // false
  ```

- in运算符只能检查某个属性或方法是否可以被对象访问，不能检查是否是自己的属性或方法

  ```js
  console.log('name' in xiaoqiang)  // true
  console.log('age' in xiaoqiang)  // true
  console.log('nationality' in xiaoqiang)  // true
  ```

#### prototype上添加方法

把方法直接添加到实例身上的缺点：每个实例和每个实例的方法函数**都是内存中不同的函数，造成了内存的浪费**

解决办法：**将方法写到prototype上**

```js
function People(name, age, sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
}
People.prototype.seyHello = function(){
    console.log('我是'+ this.name + '，我' + this.age + '岁了!');
}
People.prototype.growup = function(){
    this.age ++;
}
var xiaoqiang = People('小强', 12, '男')
var xiaohua = Penple('小花', 11, '女')
xiaoqiang.seyHello()  // 我是小强，我12岁了!
xiaohua.seyHello()  // 我是小花，我11岁了!
xiaohua.growup()
xiaohua.growup()
xiaohua.seyHello()  // 我是小花，我13岁了!
```

#### 原型链的终点

![原型链的终点](\Assets\原型链的终点.png)

#### 数组的原型链

![数组的原型链](\Assets\数组的原型链.png)



#### 继承

- 继承描述两个类之间的“is a kind of”关系，比如学生“是一种”人，所以人类和学生类之间就构成继承关系
- People是“父类”（或“超类”、“基类”）；Student是“子类”（或“派生类”）
- 子类丰富了父类，让类描述得更具体、更细化

##### 实现继承

- 实现继承的关键在于：子类必须拥有父类的全部属性和方法，同时子类还应该定义自己特有的属性和方法
- 使用JavaScript特有的原型链特性来实现继承，是普遍的做法
- ES6，还有新的实现继承的方法

```js
// 父类
function People(name, sex, age) {
	this.name = name;
	this.sex = sex;
	this.age = age;
}
People.prototype.sayHello = function () {
	console.log('你好，我是' + this.name + '今年' + this.age + '岁了');
}
People.prototype.sleep = function () {
	console.log(this.name + '正在睡觉');
}

// 子类
function Student(name, sex, age, school, sid) {
	// 借助构造函数
	People.call(this, name, sex, age);
	this.school = school;
	this.sid = sid;
}
// 关键语句，实现继承
Student.prototype = new People();  // 借助原型链，实现继承，实现两个类关联
Student.prototype.exam = function() {
	console.log(this.name + '正在考试');
};
// 重写、复写（override）父类的sayHello方法
Student.prototype.sayHello = function() {
	console.log('敬礼！你好，我是' + this.name + '今年' + this.age + '岁了，我是' + this.school + '学校的学生');
};
// 实例化
var xiaoming = new Student('小明', '男', 12, '小慕学校', 100666);
xiaoming.sayHello();
xiaoming.sleep();
xiaoming.exam();
```

**实现继承的关键语句就是，让子类的prototype指向父类的某个实例**

### 五、面向对象-红绿灯小案例

- 面向对象的本质：**定义不同的类，让类的实例工作**

- 面向对象的优点：**程序编写更清晰、代码结构更严密、使代码更健壮更利于维护**

- 面向对象经常用到的场合：**需要封装和复用性的场合（组件思维）**

- 使用面向对象编程，就能以“组件化”的思维解决大量红绿灯互相冲突的问题

- 面对对象编程，最重要的就是编写类

  

#### 红绿灯案例

- 思考：红绿灯TrafficLight类有哪些属性和方法？
- 属性：自己的当前颜色color、自己的DOM元素dom
- 方法：初始化init()、切换颜色chageColor()、绑定事件bindEvent()

```js
// 定义红绿灯类
function TrafficLight() {
	// 颜色属性，一开始都是红色
	// 红色1、黄色2、绿色3
	this.color = 1;
	// 调用自己的初始化方法
	this.init();
	// 绑定监听
	this.bindEvent();
}
// 初始化方法
TrafficLight.prototype.init = function() {
	// 创建自己的DOM
	this.dom = document.createElement('img');
	// 设置src属性
	this.dom.src = 'images/' + this.color + '.jpg';
    // 挂载dom
	box.appendChild(this.dom);
};
// 绑定监听
TrafficLight.prototype.bindEvent = function() {
	// 备份上下文，这里的this指的是JS的实例
	var self = this;
	// 当自己的dom被点击的时候
	this.dom.onclick = function () {
		// 当被点击的时候，调用自己的changeColor方法
		self.changeColor();
	};
}
// 改变颜色
TrafficLight.prototype.changeColor = function () {
	// 改变自己的color属性，从而有一种“自治”的感觉，自己管理自己，不干扰别的红绿灯
	this.color ++;
	if (this.color == 4) {
		this.color = 1;
	}
	// 光color属性变化没有用，还要更改自己的dom的src属性
	this.dom.src = 'images/' + this.color + '.jpg';
};
// 得到盒子
var box = document.getElementById('box');
// 实例化100个
var count = 100;
while(count--){  // 条件循环，当count为0时，条件为假循环终止
	new TrafficLight();  // 满足条件，添加一个新的实例
}
```

#### 炫彩小球案例

- 首先时编写Ball类，考虑类的属性和方法
  - Ball类的属性
  - 圆心坐标x、圆心坐标y、圆的半径r、透明度opacity、颜色color、DOM元素dom
  - Ball类的方法
  - 初始化init()、更新update()
- 如何实现多个小球动画？
  - 把每个小球实例都放在同一个数组种[{小球实例}，{小球实例}，...]
  - 只需要使用1个定时器，在每一帧遍历每个小球，调用它们的update方法

```js
// 小球类
function Ball(x, y) {
	// 属性x、y表示的是圆心的坐标
	this.x = x;
	this.y = y;
	// 半径属性
	this.r = 20;
	// 透明度
	this.opacity = 1;
	// 小球背景颜色，从颜色数组中随机选择一个颜色
	this.color = colorArr[parseInt(Math.random() * colorArr.length)];
	// 这个小球的x增量和y的增量，使用do while语句，可以防止dX和dY都是零
	do {
		this.dX = parseInt(Math.random() * 20) - 10;
		this.dY = parseInt(Math.random() * 20) - 10;
	} while (this.dX == 0 && this.dY == 0)
	// 初始化
	this.init();
	// 把自己推入数组，注意，这里的this不是类本身，而是实例
	ballArr.push(this);
}
// 给小球的原型添加初始化方法
Ball.prototype.init = function () {
	// 创建自己的dom
	this.dom = document.createElement('div');
	this.dom.className = 'ball';
	this.dom.style.width = this.r * 2 + 'px';
	this.dom.style.height = this.r * 2 + 'px';
	this.dom.style.left = this.x - this.r + 'px';
	this.dom.style.top = this.y - this.r + 'px';
	this.dom.style.backgroundColor = this.color;
	// 上树
	document.body.appendChild(this.dom);
};
// 更新方法，就是动态变化
Ball.prototype.update = function () {
	// 位置改变
	this.x += this.dX;
	this.y -= this.dY;
	// 半径改变
	this.r += 0.2;
	// 透明度改变
	this.opacity -= 0.01;
	this.dom.style.width = this.r * 2 + 'px';
	this.dom.style.height = this.r * 2 + 'px';
	this.dom.style.left = this.x - this.r + 'px';
	this.dom.style.top = this.y - this.r + 'px';
	this.dom.style.opacity = this.opacity;

	// 当透明度小于0的时候，就需要从数组中删除自己，DOM元素也要删掉自己
	if (this.opacity < 0) {
		// 从数组中删除自己
		for (var i = 0; i < ballArr.length; i++) {
			if (ballArr[i] == this) {
				ballArr.splice(i, 1);
			}
		}
		// 还要删除自己的dom
		document.body.removeChild(this.dom);
	}
};
// 把所有的小球实例都放到一个数组中
var ballArr = [];
// 初始颜色数组
var colorArr = ['#66CCCC', '#CCFF66', '#FF99CC', '#FF6666', '#CC3399', '#FF6600'];
// 定时器，负责更新所有的小球实例
setInterval(function () {
	// 遍历数组，调用调用的update方法
	for (var i = 0; i < ballArr.length; i++) {
		ballArr[i].update();
	}
}, 20);
// 鼠标指针的监听
document.onmousemove = function (e) {
	// 得到鼠标指针的位置
	var x = e.clientX;
	var y = e.clientY;
	new Ball(x, y);  // 实例化一个小球
};
```

### 六、内置对象

#### 包装类

- Number()、String()和Boolean()分别时数字、字符串、布尔值的**"包装类"**
- 很多编程语言都有“包装类”的设计，**包装类的目的就是为了让基本类型值可以从它们的构造函数的prototype上获得方法**
- Number()、String()和Boolean()的实例都是object类型，它们的PrimitiveValue属性存储它们的本身值
- new出来的基本类型值可以正常参与运算

#### Math(数学)对象

##### Math对象的方法

- 幂和平方：Math.pow()、Math.sqrt()

- 向上取整和向下取整：Math.ceil()、Math.floor()

- 四舍五入Math.round()可以将一个数字四舍五入为整数

  - Math.round(3.4);  // 3

  - Math.round(3.5);  // 4

  - 保留2位小数：
    $$
    3.6482^{乘100}364.82^{四舍五入}365^{除100}3.65
    $$

- 最大值Math.max()可以得到参数列表的最大值

  - Math.max(6，2，9，4)；// 9

  - **Math.max()要求参数必须是“罗列出来”，而不能使数组**

  - 涉及数组时，采用apply方法，它可以指定函数的上下文，**并且以数组形式传入“零散值”当作函数的参数**

    ```js
    var arr = [6，2，9，4];
    var max = Math.max.apply(null, arr)  // 9
    ```

- 最小值Math.min()可以得到参数列表的最小值

  - Math.min(6，2，9，4)；// 2
  - 涉及数组时同上~！

- 随机数Math.random()可以得到0~1之间的小数

  - 为了得到[a, b]区间内的整数，可以使用这个公式

    ```js
    parseInt(Math.random() * (b - a + 1)) + a
    ```

    

#### Date(日期)对象

- 使用new Date()即可得到当前时间的日期对象，它是object类型值
- 使用new Date(2022, 11, 1)即可得到指定日期的日期对象，注意第二个参数表示月份，从0开始算，11表示12月
- 也可以是new Date('2022-12-01')的写法，注意：月和日必须是两位，不足补0

##### 日期对象的常见的方法

| 方法          | 功能           |
| ------------- | -------------- |
| getDate()     | 得到日期1~31   |
| getDay()      | 得到星期0~6    |
| getMonth()    | 得到月份0~11   |
| getFullYear() | 得到年份       |
| getHours()    | 得到小时数0~23 |
| getMinutes()  | 得到分钟数0~59 |
| getSeconds()  | 得到秒数0~59   |

##### 时间戳

- 时间戳表示1970年1月1日零点整距离某时刻的毫秒数

- 通过getTime()方法或者Date.parse()函数可以将日期对象变为时间戳

  ```js
  var d = new Date()  // 获得当前日期对象
  // 显示时间戳的两种方法，时间戳表示1970年1月1日零点整距离当前时刻的毫秒数
  var timestamp1 = d.getTime();    // 精确到毫秒
  var timestamp2 = Date.parse(d);  // 精确到秒
  ```

- 通过new Date(时间戳)的写法，将时间戳变为日期对象

  ```js
  var dd = new Data(1672653710776);
  console.log(dd);  // Mon Jan 02 2023 18:01:50 GMT+0800
  console.log(dd.getFullYear());  // 2023
  ```

  

### 七、【拓展】继承与内置构造函数

#### 内置构造函数

- JavaScript有很多**内置构造函数**，比如Array就是数组类型的构造函数，**Function**就是函数类型的构造函数，**Object**就是对象类型的构造函数
- 内置构造函数非常有用，所有**该类型的方法都是定义在它的内置构造函数的prototype上的**，我们可以给这个对象添加新的方法，从而拓展某类型的功能

```js
// 数组的内置构造函数，任何的数组字面量都可以看做是Array的实例
console.log([1, 2] instanceof Array);  // true
console.log([] instanceof Array);  // true

var arr = new Array(5);
console.log(arr);  // （5）[empty * 5]
console.log(arr.length);  // 5

// 函数的内置构造函数，任何的函数字面量都可以看做是Function的实例
function fun() {

}
function add(a, b) {
	return a + b;
}
console.log(fun instanceof Function);  // true
console.log(add instanceof Function);  // true

var jianfa = new Function('a', 'b', 'return a - b');
console.log(jianfa(8, 3));  // 5

// 对象的内置构造函数
console.log({a: 1} instanceof Object);  // true
console.log({} instanceof Object);  // true

var o = new Object();
o.a = 2;
o.b = 6;
console.log(o);  // {a:2, b:6}
```

#### 内置构造函数的关系

##### Object.prototype是万物原型链的终点

Object.prototype是万物原型链的终点。JavaScript种函数、数组皆为对象，以数组为例，完整原型链是这样的：

![数组的原型链02](\Assets\数组的原型链02.png)

```js
console.log([1,2,3].__proto__ === Array.prototype);  // true
console.log([1,2,3].__proto__.__proto__ === Object.prototype);  // true

console.log([] instanceof Object);  // true
console.log([] instanceof Array);  // true

console.log(Object.prototype.__proto__);  // null
console.log(null.__proto__);  // 报错
```

任何函数都可以看做是Funciton“new出来的”，那我们开一个脑洞：Object也是函数，它是不是Functionc“new出来的呢”？答案是肯定的

```js
console.log(Object.__proto__ === Function.prototype);
console.log(Object.__proto__.__proto__ === Object.prototype);
console.log(Function.__proto__ === Function.prototype);

console.log(Function instanceof Object);        // true
console.log(Object instanceof Function);        // true
console.log(Function instanceof Function);      // true
console.log(Object instanceof Object);          // true
```

#### 继承

- People类拥有的属性和方法Student类**都有**，Student类还扩展了一些属性的方法
- Student"是一种"People，两类之间是"is a kind of"关系
- 这就是继承关系：Student类继承自People类

- 继承描述两个类之间的“is a kind of”关系，比如学生“是一种”人，所以人类和学生类之间就构成继承关系
- People是“父类”（或“超类”、“基类”）；Student是“子类”（或“派生类”）
- 子类丰富了父类，让类描述得更具体、更细化

##### 通过原型链继承

![过原型链实现继承](\Assets\通过原型链实现继承.png)

```js
// 父类：People类
function People(name, age, sex) {
	// this.arr = [33, 44, 55];
	this.name = name;
	this.age = age;
	this.sex = sex;
}
People.prototype.sayHello = function () {
	console.log('你好，我是' + this.name + '我今年' + this.age + '岁了');
};
People.prototype.sleep = function () {
	console.log(this.name + '正在睡觉');
};
// 子类：Student类
function Student(name, age, sex, school, sid) {
	this.name = name;
	this.age = age;
	this.sex = sex;
	this.school = school;
	this.sid = sid;
}
// 实现继承的非常重要的语句。让子类的prototype指向父类的一个实例。
Student.prototype = new People();  // 这条语句一定要写在子类的构造函数后面
// 追加方法
Student.prototype.exam = function () {
	console.log(this.name + '正在考试');
};
Student.prototype.study = function () {
	console.log(this.name + '正在学习');
};
// 子类可以更改父类的方法，术语叫做override“改写”、“重写”
Student.prototype.sayHello = function () {
	console.log('敬礼！您好，我是' + this.name + '，我是' + this.school + '的学生，我' + this.age + '岁了');
};

var xiaoming = new Student('小明', 12, '男', '小慕学校', 100666);
xiaoming.exam();
xiaoming.study();
xiaoming.sayHello();
xiaoming.sleep();
// xiaoming.arr.push(123);
// console.log(xiaoming.arr);

var xiaohong = new Student('小红', 11, '女', '小慕学校', 100667);
xiaohong.exam();
xiaohong.study();
xiaohong.sayHello();
xiaohong.sleep();
// console.log(xiaohong.arr);

var laowang = new People('老王', 56, '男');
laowang.sayHello();
```

##### 通过原型链继承的问题

- 问题1：如果父类的属性中有引用类型值，则这个属性会被所有子类的实例共享
- 问题2：子类的构造函数中，往往需要重复定义很多超类定义过的属性。即，子类的构造函数写的不够优雅

##### 借用构造函数

- 为了解决原型中包含引用类型值所带来的问题和子类构造函数不优雅的问题，开发人员通常使用一种叫做“**借助构造函数**”的技术，也被称为“**伪造对象**”或“**经典继承**”
- 借用构造函数的思想非常简单：**在子类构造函数的内部调用超类的构造函数**，但是要注意使用call()绑定上下文
- 通过借用构造函数解决原型链继承的共享问题和代码优雅问题

```js
// 父类
function People(name, sex, age) {
	this.name = name;
	this.sex = sex;
	this.age = age;
    // 这个引用类型arr,会被call()写在每个实例身上，不再是共享性质
	this.arr = [33, 44, 55];  
}
People.prototype.sayHello = function () {
	console.log('你好，我是' + this.name + '今年' + this.age + '岁了');
}
People.prototype.sleep = function () {
	console.log(this.name + '正在睡觉');
}
// 子类
function Student(name, sex, age, school, sid) {
    // 借助构造函数
	People.call(this, name, sex, age);
	this.school = school;
	this.sid = sid;
}
// 实现继承，借助原型链
Student.prototype = new People();
Student.prototype.exam = function() {
	console.log(this.name + '正在考试');
};
Student.prototype.sayHello = function() {
	console.log('敬礼！你好，我是' + this.name + '今年' + this.age + '岁了，我是' + this.school + '学校的学生');
};
var xiaoming = new Student('小明', '男', 12, '小慕学校', 100666);
console.log(xiaoming);
xiaoming.arr.push(77);
console.log(xiaoming.arr);  // [33, 44, 55， 77]
// 通过hasOwnProperty()方法检查，对象身上是否有arr这个属性
console.log(xiaoming.hasOwnProperty('arr'));  // true
xiaoming.sayHello();
xiaoming.sleep();
xiaoming.exam();

var xiaohong = new Student('小红', '女', 11, '小慕学校', 100667);
console.log(xiaohong.arr);  // [33, 44, 55]
console.log(xiaohong.hasOwnProperty('arr'));  // true
```

> 借助构造函数，解决共享问题和代码优雅问题

##### 组合继承

- 将借用原型链和借用构造函数的技术组合在一起，叫做**组合继承**，也叫做**伪经典继承**
- 组合继承是JavaScript中最常用的继承模式
- 缺点：组合继承最大的问题就是无论什么情况下，都会调用两次超类的构造函数：
  - 一次是在创建子类原型的时候
  - 另一次是在子类构造函数的内部

##### 原型式继承

###### Object.create()

IE9开始支持Object.create()方法，可以**根据指定的对象位原型创建出新对象**

`var obj2 = Object.create(obj1);`

第二个参数：必须是对象形式{name: {value: xxx}}

```js
var obj1 = {
	a: 33,
	b: 45,
	c: 12,
	test: function() {
		console.log(this.a + this.b);
	}
};
var obj2 = Object.create(obj1, {
	d: {
		value: 99
	}, 
	a: {
		value: 2
	}
});
console.log(obj2.__proto__ === obj1);       // true
console.log(obj2.a);
console.log(obj2.b);
console.log(obj2.c);
console.log(obj2.d);

obj2.test();
```

在没有必要“兴师动众”地创建构造函数，而只是想让新对象与现有对象“类似”的情况下，使用Object.create()即可胜任，称为原型式继承

###### Object.create()的兼容性写法

兼容低版本的IE

```js
// 道格拉斯·克罗克福德写的一个函数，非常巧妙，面试常考
// 函数的功能就是以o为原型，创建新对象
function object(o) {
	// 创建一个临时构造函数
	function F() {}
	// 让这个临时构造函数的prototype指向o，这样它new出来的对象，__proto__指向了o
	F.prototype = o;
	// 返回F的实例
	return new F();
}
var obj1 = {
	a: 23,
	b: 5
};
var obj2 = object(obj1);
console.log(obj2.__proto__ === obj1);
console.log(obj2.a);
console.log(obj2.b);
```

##### 寄生式继承

寄生式继承：编写一个函数，它接收一个参数o，返回以o为原型的新对象p，同时给p上添加预置的新方法

寄生式继承就是编写一个函数，它可以“增强对象”，只要把对象传入这个函数，这个函数将以此对象为“基础”创建出新对象，并为新对象赋予新的预置方式

在主要考虑对象而不是自定义类型和构造函数的情况下，寄生式基础也是一种有用的模式

寄生式继承的缺点：使用寄生式继承来为对象添加函数，会由于不能做到函数复用而降低效率，即"方法没有写到prototype上"

```js
var o1 = {
	name: '小明',
	age: 12,
	sex: '男'
};
var o2 = {
	name: '小红',
	age: 11,
	sex: '女'
};
// 寄生式继承
function f(o) {
	// 以o为原型创建出新对象
	var p = Object.create(o);
	// 补充方法
	p.sayHello = function () {
		console.log('你好，我是' + this.name + '今年' + this.age + '岁了');
	}
	p.sleep = function () {
		console.log(this.name + '正在睡觉');
	}
	return p;
}
var p1 = f(o1);
p1.sayHello();
var p2 = f(o2);
p2.sayHello();
console.log(p1.sayHello == p2.sayHello);
```

##### 寄生组合式继承

- 寄生组合式继承：通过借用构造函数来继承属性，通过原型链的混成形式来继承方法
- 其背后的基本思路是：不必为了指定子类型的原型而调用超类型的构造函数，**我们所需要的无非就是超类型原型的一个副本而已**。本质上，就是**使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型的原型**。

![寄生组合式继承](\Assets\寄生组合式继承.png)

```js
// 这个函数接收两个参数，subType是子类的构造函数，superType是父类的构造函数
function inheritPrototype(subType, superType) {
    // Object.create根据父类原型创建一个新的对象
	var prototype = Object.create(superType.prototype);
    // 将子类的原型指向新的对象原型，实现继承
	subType.prototype = prototype;
}
// 父类
function People(name, sex, age) {
	this.name = name;
	this.sex = sex;
	this.age = age;
}
People.prototype.sayHello = function () {
	console.log('你好，我是' + this.name + '今年' + this.age + '岁了');
}
People.prototype.sleep = function () {
	console.log(this.name + '正在睡觉');
}
// 子类
function Student(name, sex, age, school, sid) {
	// 借助构造函数
	People.call(this, name, sex, age);
	this.school = school;
	this.sid = sid;
}
// 调用我们自己编写的inheritPrototype函数，这个函数可以让Student类的prototype指向“以People.prototype为原型的一个新对象”
inheritPrototype(Student, People);
Student.prototype.exam = function() {
	console.log(this.name + '正在考试');
};
Student.prototype.sayHello = function() {
	console.log('敬礼！你好，我是' + this.name + '今年' + this.age + '岁了，我是' + this.school + '学校的学生');
};
var xiaoming = new Student('小明', '男', 12, '小慕学校', 100666);
xiaoming.sleep();
xiaoming.exam();
xiaoming.sayHello();
```

##### instanceof运算符

- instanceof运算符用来检测“某对象是不是某个类的实例”，
  - 比如：xiaoming instanceof Student   // 检测xiaoming是不是Student类的实例
- 底层机理：**检查Student.prototype属性是否在xiaoqiang的原型链上**（多少层都行，只要在就行）

#### 面向对象的重点内容

- 熟悉每天函数上下文this的判定规则
- call和apply的功能和区别
- 用new调用函数的四步走
- 什么是类和实例？面向对象编程的意义
- prototype和原型链查找
- 继承的实现
- 使用面向对象实现小案例-->反复练习
- 熟练掌握Math、Date等JS内置对象

## 正则表达式

正则表达式 (regular expression)描述了字符串“构成模式”，经常被用于检查字符串是否符合预定的格式要求

演示正则表达式基本使用方法：检查某个字符串是否是6位数字

```js
// 要检查的字符串
var str = '123456';
// 设置正则表达式规则
var regexp = /^\d{6}&/;
// 检查
if(regexp.test(str)){
    console.log('符合要求')
}else{
    console.log('不符合要求')
}
```

### 正则表达式的创建

- 使用**/内容/**的语法形式，可以快捷创建正则表达式
- 也可以使用**new RegExp('内容')**的形式，创建正则表达式 
- 使用**typeof运算符检查正则表达式的类型，结果是object**

```js
// 创建正则表达式
var regexp1 = /^\d{6}&/;
var regexp2 = new RegExp('\\d{6}&');  // 字符串内两个\代表一个\
```

### 元字符

“元字符”是指一位指定类型的字符

| 元字符 | 功能                                       |
| ------ | ------------------------------------------ |
| \d     | 匹配一个数字                               |
| \D     | 匹配一个非数字字符                         |
| \w     | 匹配一个单字字符（字母、数字或下划线）     |
| \W     | 匹配一个非单字字符                         |
| \s     | 匹配一个空白字符，包括空格、制表符和换行符 |
| .      | 任意字符                                   |

- 开头和结尾

| 元字符 | 功能     |
| ------ | -------- |
| ^      | 匹配开头 |
| $      | 匹配结尾 |

> 如果使用new RegExp()写法，反斜杠需要多写一个

### 字符的转义

- 在特殊字符之前的反斜杠\表示下一个字符不是特殊字符，应该按照字面理解

### 方括号表示法

- 使用方括号，比如[xyz]，可以创建一个字符集合，表示匹配方括号中的任意字符
- 可以使用短横-来指定一个字符范围，^表示否定

| 元字符 | 等价的方括号表示法 |
| ------ | ------------------ |
| \d     | [0-9]              |
| \D     | [^0-9]             |
| \w     | [A-Za-z0-9_]       |
| \W     | [^A-Za-z0-9_]      |

```js
// 某学校的学号规定：第1位是一个字母，b表示本科生，y表示研究生，后面是7位数字，用正则表示为：
// 学号字符串
var str1 = 'b4444555';
// 用正则表达式进行检查
console.log(/^[by]\d{7}$/.test(str1));  // true
// *******************************************
// 题目1：请验证某字符串是否是5位字母，大小写均可
var str2 = 'abcde';
var str3 = 'abcd5';
console.log(/^[a-zA-Z]{5}$/.test(str2));  // true
console.log(/^[a-zA-Z]{5}$/.test(str3));  // false
// 题目2：请验证某字符串是否是5位，且仅由小写字母、点构成
var str4 = 'mnp..';
var str5 = 'mnp.#';
console.log(/^[a-z\.]{5}$/.test(str4));  // true
console.log(/^[a-z\.]{5}$/.test(str5));  // false
// 题目3：请验证某字符串是否是4位小写字母，且最后一位不能是m字母
var str6 = 'abcd';
var str7 = 'abcm';
var str8 = 'ab1c';
console.log(/^[a-z]{3}[a-ln-z]$/.test(str6));  // true
console.log(/^[a-z]{3}[a-ln-z]$/.test(str7));  // false
console.log(/^[a-z]{3}[a-ln-z]$/.test(str8));  // true
```

### 量词

| 量词  | 意义                                           |
| ----- | ---------------------------------------------- |
| *     | 匹配前一个表达式0次或多次。等价于{0,}          |
| +     | 匹配前面一个表达式1次或者多次。等价于{1,}      |
| ？    | 匹配前面一个表达式0次或者1次。等价于{0,1}      |
| {n}   | n是一个正整数，匹配了前面一个字符刚好出现了n次 |
| {n,}  | n是一个正整数，匹配了前一个字符至少出现了n次   |
| {n,m} | n和m都是整数。匹配前面的字符至少n次，最多m次   |

```js
// 题目1：请验证字符串是否符合手机号码的规则：11位数字，并且肯定以1开头
var str1 = '13812345678';
var str2 = '138123456789';
var str3 = '38123456789';
var regexp1 = /^1\d{10}$/;
console.log(regexp1.test(str1));
console.log(regexp1.test(str2));
console.log(regexp1.test(str3));
// 题目2：请验证某字符串是否是这样的：以字母开头，中间是任意位数字（最少1位）构成，并以字母结尾
var str4 = 'a123123123b';
var str5 = 'abcd';
var str6 = 'a1b';
var regexp2 = /^[a-zA-Z]\d+[a-zA-Z]$/;
console.log(regexp2.test(str4));
console.log(regexp2.test(str5));
console.log(regexp2.test(str6));
// 题目3：请验证某字符串是否符合网址规则：以www.开头，中间是任意位的字符（字母数字下划线，最少一位），最后以.com结尾，也可以以.com.cn结尾
var str7 = 'www.imooc.com';
var str8 = 'www.sina.com.cn';
var str9 = 'www.news.cn';
var regexp3 = /^www\.\w+\.com(\.cn)?$/;
console.log(regexp3.test(str7));
console.log(regexp3.test(str8));
console.log(regexp3.test(str9));
```

### 修饰符

修饰符也叫标志(flags)，用于使用正则表达式实现高级搜索

| 修饰符 | 意义             |
| ------ | ---------------- |
| i      | 不区分大小写搜索 |
| g      | 全局搜索         |

- 修饰符的使用

  ```js
  var re = /m/gi;  // 第一种写法
  var re = new RegExp('m', 'gi')  // 第二种写法
  ```

  

### 正则表达式的相关方法

正则表达式可以“打点”调用的方法：

| 方法   | 简介                                                     |
| ------ | -------------------------------------------------------- |
| test() | 测试某字符串是否匹配正则表达式，返回布尔值               |
| exec() | 根据正则表达式，在字符串中进行查找，返回结果数组或者null |

- 正则表达式的test()方法用来**测试某字符串是否匹配此正则表达式**，它返回true或false

- exec()方法功能是：在一个指定字符串中执行一个**搜索匹配查找**，返回一个结果信息数组或null

  ```js
  var str = 'abc123def456ghi789';
  var regexp = /\d+/;
  var result1 = regexp.exec(str);  // {“123”，index:3,input:"abc123def456ghi789",...}
  ```

exec()方法的逐条遍历：**有“g”修饰符的正则表达式将自动成为“有状态”的**，这意味着可以对单个字符串中多次匹配结果进行**逐条的遍历**

```js
var str = 'abc123def456ghi789';
var regexp = /\d+/g;
// 会进行逐条遍历
var result1 = regexp.exec(str);  // {“123”，index:3,input:"abc123def456ghi789",...}
var result2 = regexp.exec(str);  // {“456”，index:9,input:"abc123def456ghi789",...}
var result3 = regexp.exec(str);  // {“789”，index:15,input:"abc123def456ghi789",...}
// 实际使用中会使用while循环来获取结果
while(result = regexp.exec(str)){  // 当resule = null为假则退出循环
    console.log(resule);
}
```

### 字符串的相关方法

| 方法      | 简介                                                         |
| --------- | ------------------------------------------------------------ |
| search()  | 在字符串中根据正则表达式进行查找匹配，返回首次匹配到的位置索引，测试不到则返回-1 |
| match()   | 在字符串中根据正则表达式进行查找匹配，返回一个数组，找不到则返回null |
| replace() | 使用替换字符串替换掉匹配到的子字符串，可以使用正则表达式     |
| split()   | 分隔字符串为数组，可以使用正则表达式                         |

```js
var str = 'abc123def4567ghi89';

// search()方法，很像indexOf()，返回查找到的第一个下标，如果找不到就是-1
var result1 = str.search(/\d+/g);
var result2 = str.search(/m/g);
console.log(result1);       // 3
console.log(result2);       // -1

// match()方法，返回查找到的数组，找不到就是null
var result3 = str.match(/\d+/g);
console.log(result3);       // ["123", "4567", "89"]

// replace()方法，进行替换
var result4 = str.replace(/[a-z]+/g, '*');      // 注意+表示贪婪的，尽可能多的连续匹配小写字母
console.log(result4);       // *123*4567*89

// split()方法，进行字符串拆为数组
var result5 = str.split(/\d+/g);
console.log(result5);       // ["abc", "def", "ghi", ""]
```

### 正则表达式的应用

- 用正则表达式进行表单验证是正则表达式最重要的实际应用
- 实际上，很多正则表达式不需要我们自己写，可以通过搜索引擎查找，可以拿来即用

```html
<style>
	.warning {
		color: red;
		display: none;
	}
</style>
<div>
	<p>
		请输入中文姓名：
		<input type="text" id="nameField">
		<span class="warning" id="nameWarning">输入的姓名不合法</span>
	</p>
	<p>
		请输入手机号码：
		<input type="text" id="telField">
		<span class="warning" id="telWarning">输入的手机号码不合法</span>
	</p>
	<p>
		请输入Email：
		<input type="text" id="emailField">
		<span class="warning" id="emailWarning">输入的Email不合法</span>
	</p>
</div>
<script>
	var nameField = document.getElementById('nameField');
	var telField = document.getElementById('telField');
	var emailField = document.getElementById('emailField');
	var nameWarning = document.getElementById('nameWarning');
	var telWarning = document.getElementById('telWarning');
	var emailWarning = document.getElementById('emailWarning');

	// 当文本框失去焦点，就是光标不在文本框中了
	nameField.onblur = function () {
		// 得到姓名
		var name = nameField.value;
		if (/^[\u4E00-\u9FA5]{2,4}$/.test(name)) {
			// 如果通过校验
			nameWarning.style.display = 'none';
		} else {
			// 如果没有通过校验
			nameWarning.style.display = 'inline';
		}
	};
	telField.onblur = function () {
		// 得到电话
		var tel = telField.value;
		if (/^1\d{10}$/.test(tel)) {
			// 如果通过校验
			telWarning.style.display = 'none';
		} else {
			// 如果没有通过校验
			telWarning.style.display = 'inline';
		}
	};
	emailField.onblur = function () {
		// 得到email
		var email = emailField.value;
		// 合法的email都是abc_def123@abc.net

		if (/^\w{2,}\@\w{2,}\.[a-z]{2,4}(\.[a-z]{2,4})?$/.test(email)) {
			// 如果通过校验
			emailWarning.style.display = 'none';
		} else {
			// 如果没有通过校验
			emailWarning.style.display = 'inline';
		}
	};
</script>
```

### 总结：重点内容

- 元字符、量词、方括号表示法必须要熟悉
- 正则表达式和字符串的常用方法要熟悉
- 可以用百度等搜索引擎查找常用正则表达式
