## `<script>`注意事项

如果想输出一个`</script>`字符串，需要把字符串分成多个部分，通过连接符`+`来连接，否则浏览器会误解成`JavaScript`代码已经结束了。**注意在单独的`*.js`文件中不需要这样处理。**

```
<script type="text/javascript">
alert('</scr'+'ipt>');
</script>
```

使用`src`引用外部`*.js`文件的时候必须使用`</script>`，不能是`/>`结尾。在`script`之间添加的任何`JavaScript`代码都不会被执行。

```
<script type="text/javascript" src="xxx.js"></script> //正确用法
<script type="text/javascript" src="xxx.js"/> //错误用法
<script type="text/javascript" src="xxx.js">
alert('不会被执行！！！');
</script>
```

## 标识符

[[Back To Top]](#jump-to-section)

标识符用来对变量、函数、属性等进行命名。标识符命名规则如下：

 - 第一字符必须是字母、下划线`_`、美元符号`$`。
 - 其他字符可以是字母、下划线`_`、美元符号`$`或数字。
 - 不能把关键字、保留字作为标识符。
 - `JavaScript`区分大小写。

## 运算符

[[Back To Top]](#jump-to-section)

**typeof**
- 语法`typeof [(] expression [)]`
- 操作符返回一个字符串，括号是可有可无的

 ```
 | Type          | Result        |
 | ------------- |:-------------:|
 | Undefined     | "undefined"   |
 | null          | "object"      |
 | Boolean       | "boolean"     |
 | String        | "string"      |
 | Number        | "number"      |
 | Object        | "object"      |
 | Array         | "object"      |
 | Function      | "function"    |
 ```

- 用法

 ```
 // Numbers
 typeof 37 === 'number';
 typeof 3.14 === 'number';
 typeof Math.LN2 === 'number';
 typeof Infinity === 'number';
 typeof NaN === 'number'; // 尽管NaN是"Not-A-Number"的缩写,意思是"不是一个数字"
 typeof Number(1) === 'number'; // 不要这样使用!

 // Strings
 typeof "" === 'string';
 typeof "bla" === 'string';
 typeof (typeof 1) === 'string'; // typeof返回的肯定是一个字符串
 typeof String("abc") === 'string'; // 不要这样使用!

 // Booleans
 typeof true === 'boolean';
 typeof false === 'boolean';
 typeof Boolean(true) === 'boolean'; // 不要这样使用!

 // Undefined
 typeof undefined === 'undefined';
 typeof blabla === 'undefined'; // 一个未定义的变量,或者一个定义了却未赋初值的变量

 // Objects
 typeof {a:1} === 'object';
 typeof [1, 2, 4] === 'object'; // 使用Array.isArray或者Object.prototype.toString.call方法可以分辨出一个数组和真实的对象
 typeof new Date() === 'object';

 typeof new Boolean(true) === 'object' // 令人困惑.不要这样使用
 typeof new Number(1) === 'object' // 令人困惑.不要这样使用
 typeof new String("abc") === 'object';  // 令人困惑.不要这样使用

 // Functions
 typeof function(){} === 'function';
 typeof Math.sin === 'function';

 // null
 typeof null === 'object'; // 从JavaScript诞生以来,一直是这样的.
 ```

***

**算术运算符**

- `+`：对数字进行加法运算或者连接字符串

 ```
 // Number + Number -> 加法运算
 1 + 2 // 7

 // Boolean + Number -> 加法运算
 true + 1 // 2

 // Boolean + Boolean -> 加法运算
 false + false // 0

 // Number + String -> 连接字符串操作
 5 + "foo" // "5foo"

 // String + Boolean -> 连接字符串操作
 "foo" + false // "foofalse"

 // String + String -> 连接字符串操作
 "foo" + "bar" // "foobar"
 ```

- `-`：减法

 ```
 5 - 3 // 2
 3 - 5 // -2
 "foo" - 3 // NaN
 1 - NaN // NaN，只要有一个NaN就为NaN
 -100 - -70 // -30，即：-100 - (-70)
 100 - true // 99，true转成数值为1
 ```

- `*`：乘法

 ```
 2 * 2 // 4
 -2 * 2 // -4
 Infinity * 0 // NaN
 Infinity * Infinity // Infinity
 "foo" * 2 // NaN

 100 * true // 100，true 转成数值为1
 100 * '' // 0，''转成了0
 100 * null // 0，null 转成了0
 ```

- `/`：除法

 ```
 1 / 2      // 0.5
 1.0 / 2.0  // 0.5
 2.0 / 0    // Infinity
 2.0 / 0.0  // Infinity
 2.0 / -0.0 // -Infinity

 100 / 70 // 1.42....
 100 / NaN // NaN
 Infinity / Infinity // NaN
 -Infinity / Infinity // NaN
 -Infinity / -Infinity // NaN
 100 / true // 100，true 转成1
 100 / '' // Infinity
 100 / null // Infinity
 100 / 'Lee' // NaN
 100 / 对象 // NaN，如果有toString()或valueOf()，则返回10 / 返回数的值
 ```

- `%`：取模

 ```
 12 % 5 // 2
 -1 % 2 // -1
 NaN % 2 //

 10 % 3 // 1，余数为1
 100 % NaN // NaN
 Infinity % Infinity // NaN
 -Infinity % Infinity // NaN
 -Infinity % -Infinity // NaN
 100 % true // 0
 100 % '' // NaN
 100 % null // NaN
 100 % 'Lee' // NaN
 ```

- `++`：自增

 ```
 // 先赋值再自增
 var x = 3;
 y = x++; // y = 3, x = 4

 // 先自增再赋值
 var a = 2;
 b = ++a; // a = 3, b = 3
 ```

- `--`：自减

 ```
 // 先赋值再自减
 var x = 3;
 y = x--; // y = 3, x = 2

 // 先自减再赋值
 var a = 2;
 b = --a; // a = 1, b = 1
 ```

- 一元运算符`-`：负数

 ```
 var x = 3;
 y = -x; // y = -3, x = 3
 ```

- 一元运算符`+`：正数

 ```
 +3     // 3
 +"3"   // 3
 +true  // 1
 +false // 0
 +null  // 0
 ```

***

**比较运算符**

比较运算符：`==, !=, ===, !==, >, >=, <, <=`

- `==`：等于只比较值，会为了比较两个值而进行强制类型转换

 ```
 ""           ==   "0"           // false
 0            ==   ""            // true
 0            ==   "0"           // true
 false        ==   "false"       // false
 false        ==   "0"           // true
 false        ==   undefined     // false
 false        ==   null          // false
 null         ==   undefined     // true
 " \t "       ==   0             // true
 ```

- `===`：恒等于不仅比较值，而且还比较值的类型，不会进行强制类型转换

 ```
 ""           ===   "0"           // false
 0            ===   ""            // false
 0            ===   "0"           // false
 false        ===   "false"       // false
 false        ===   "0"           // false
 false        ===   undefined     // false
 false        ===   null          // false
 null         ===   undefined     // false
 " \t "       ===   0             // false
 ```

***

**逻辑运算符**

- `&&`：逻辑与
 - 如果两个操作数都为boolean类型，则返回值为boolean类型
 - 如果第一个操作数的转换结果为false，则返回第一个操作数
 - 如果第一个操作数的转换结果为true，则返回第二个操作数

 ```
 a1=true && true       // t && t returns true
 a2=true && false      // t && f returns false
 a3=false && true      // f && t returns false
 a4=false && (3 == 4)  // f && f returns false
 a5="Cat" && "Dog"     // t && t returns Dog
 a6=false && "Cat"     // f && t returns false
 a7="Cat" && false     // t && f returns false
 (5 > 4) && null;      // t && null returns null
 (3 > 4) && null;      // f && null returns false
 (5 > 4) && undefined;      // t && undefined returns undefined
 (3 > 4) && undefined;      // f && undefined returns false
 ```

- `||`：逻辑或
 - 如果两个操作数都为boolean类型，则返回值为boolean类型
 - 如果第一个操作数的转换结果为true，则返回第一个操作数
 - 如果第一个操作数的转换结果为false，则返回第二个操作数

 ```
 o1=true || true       // t || t returns true
 o2=false || true      // f || t returns true
 o3=true || false      // t || f returns true
 o4=false || (3 == 4)  // f || f returns false
 o5="Cat" || "Dog"     // t || t returns Cat
 o6=false || "Cat"     // f || t returns Cat
 o7="Cat" || false     // t || f returns Cat
 ```

- `!`：逻辑非，先将这个值转换成布尔值，然后取反

 ```
 n1=!true              // !t returns false
 n2=!false             // !f returns true
 n3=!"Cat"             // !t returns false
 ```

***

**赋值运算符**

`=, *=, /=, %=, +=, -=, <<=, >>=, >>>=, &=, ^=, |=`
- 赋值运算符将右边表达式的值赋值给左边的变量

 ```
 |Shorthand operator | Meaning     |
 | x = y             | x = y       |
 | x += y            | x = x + y   |
 | x -= y            | x = x - y   |
 | x *= y            | x = x * y   |
 | x /= y            | x = x / y   |
 | x %= y            | x = x % y   |
 | x <<= y           | x = x << y  |
 | x >>= y           | x = x >> y  |
 | x >>>= y          | x = x >>> y |
 | x &= y            | x = x & y   |
 | x ^= y            | x = x ^ y   |
 | x |= y            | x = x | y   |
 ```

***

**三元运算符**

语法：`condition ? expr1 : expr2`
- 条件运算符根据condition的真假返回后面两个表达式其中的一个
- 如果条件为真，则运算符返回的值为表达式1；否则，它返回的值为表达式2

## 数据类型

[[Back To Top]](#jump-to-section)

**Undefined类型**

- 首字母大写的`Undefined`表示的是一种数据类型，小写的`undefined`表示的是属于这种数据类型的唯一的一个值
- 一个未初始化的变量的值为`undefined`，一个没有传入实参的形参变量的值为`undefined`，如果一个函数什么都不返回，则该函数默认返回`undefined`
- 一个值未定义的顶层属性；`undefined`同时也是原始值
- 使用严格相等运算符来判断一个值是否是`undefined`
 ```
 var x;
 if (x === undefined) {
    // 执行到这里
 }
 else {
    // 不会执行到这里
 }
 /*
 注意: 这里必须使用严格相等运算符===，而不能使用普通的相等运算符==，
 因为x == undefined成立还可能是因为x为null，在JavaScript中null== undefined是返回true的
 */
 ```

- 另外还可以使用`typeof`来判断
 ```
 var x;
 if (typeof x === 'undefined') {
    // 执行到这里
 }
 ```

- 有时必须使用`typeof`的原因是，如果一个变量根本没有被声明，只有使用`typeof`判断才不会报错，用相等运算符判断会抛出异常
 ```
 // x没有被声明过
 if (typeof x === 'undefined') { // 不会报错
    // these statements execute
 }

 if(x === undefined){ // 抛出ReferenceError异常

 }
 ```

***

**Null类型**

- `Null`类型是一个只有一个值的数据类型，即特殊的值`null`。它表示一个空对象引用(指针)，而`typeof null`会返回`object`
- 一个特殊的用于表示空值的关键字；同时`null`也是一个原始(`primitive`)值
- `undefined`是派生自`null`的，因此`undefined == null`返回`true`
- 如果要比较`undefined`和`null`，可以采用`typeof`方式或者`===`方式进行比较

 ```
 var box;
 var car = null;
 alert(typeof box == typeof car); // false
 alert(box === car); // false
 ```

***

**Boolean类型**

- 语法`new Boolean(value)`
- `Boolean`类型有两个值：`true`和`false`
- 不要将原始值`true/false`，和值为`true/false`的`Boolean`对象相混淆
- `0`、`-0`、`null`、`false`、`NaN`、`undefined`、空字符串`""`生成的`Boolean`对象的值为`false`；其他任何值，包括任何对象或者字符串`"false"`，都会创建一个值为`true`的`Boolean`对象
- 任何值为`undefined`或者`null`的对象，包括值为`false`的`Boolean`对象，在条件语句中，其值都将作为`true`来判断。例如，下面的条件语句中，`if`就将对象`x`看作是`true`：
 ```
 x = new Boolean(false);
 if (x) {
   // . . . 这里的代码仍会被执行
 }
 ```

- `Boolean`原始值不会有这种表现。例如，下面的条件结构中，`if`语句的内部代码不会被执行：
 ```
 x = false;
 if (x) {
   // . . . 这里的代码不会被执行
 }
 ```

- 不要通过新建`Boolean`对象的方法来将一个非布尔值转化成布尔值，直接使用`Boolean()`函数才是正确的：
 ```
 x = Boolean(expression);     // 这样用
 x = new Boolean(expression); // 而不要这样!
 ```

- 如过你用一个对象作为`Boolean`对象的初始化值，则即使该对象是个值为`false`的`Boolean`对象，生成的`Boolean`对象的值也是`true`
 ```
 myFalse = new Boolean(false);   // 初始化值为false
 g = new Boolean(myFalse);       // 初始化值为true
 myString = new String("Hello"); // string 对象
 s = new Boolean(myString);      // 初始化值为true
 ```

- 总而言之不要在该使用`Boolean`原始值的地方使用`Boolean`对象

***

**Number类型**

- 语法`new Number(value)`，如果参数`value`无法被转换为数字，则返回`NaN`
- `Number()`函数用来执行类型转换
- `Number`类型包含两种数值：整型和浮点型
 ```
 // 最常用的十进制整型
 var box = 100;

 // 八进制整型，以8为基数，第一位必须是0，八进制序列(0~7)
 var box = 070; // 八进制，56
 var box = 079; // 无效的八进制，自动解析为79
 var box = 08; // 无效的八进制，自动解析为8

 // 十六进制整型，前面两位必须是0x，后面是0~9及A~F
 var box = 0xA; // 十六进制，10
 var box = 0x1f; // 十六进制，31

 // 浮点类型，就是该数值中必须包含一个小数点，并且小数点后面必须至少有一位数字
 var box = 3.8;
 var box = 0.8;
 var box = .8; // 有效，但不推荐此写法

 // 由于保存浮点数值需要的内存空间比整型数值大两倍，因此会自动将可以转换为整型的浮点数值转成为整型
 var box = 8.; // 小数点后面没有值，转换为8
 var box = 12.0; // 小数点后面是0，转成为12

 // 对于那些过大或过小的数值，可以用科学技术法来表示(e表示法)。用e表示该数值的前面10的指数次幂
 var box = 4.12e9; // 即4120000000
 var box = 0.00000000412; // 即4.12e-9

 // 虽然浮点数值的最高精度是17位小数，但算术运算中可能会不精确（解决方法：先扩大为整数，运算之后再除以倍数）。
 alert(0.1+0.2); // 0.30000000000000004
 ```
- `Number.MAX_VALUE` 最大正数。
- `Number.MIN_VALUE` 最小正数，即最接近`0`的正数（实际上不会变成`0`）
- `-Number.MAX_VALUE` 最大的负数
- `-Number.MIN_VALUE` 最小的负数
- 如果超过了数值范围的最大值或最小值，那么就会变成正无穷`Infinity`或者负无穷`-Infinity`。要想确定一个数值到底是否超过了规定范围，可以使用`isFinite()`函数。如果没有超过，返回`true`，超过了返回`false`

 ```
 alert(Number.POSITIVE_INFINITY); // Infinity(正无穷)
 alert(Number.NEGATIVE_INFINITY); // -Infinity(负无穷)
 ```

- `Number.NaN`，即非数值（Not a Number）是一个特殊的值。任何与`NaN`进行运算的结果均为`NaN`，`NaN`不与任何值相等（包括自身不相等）

 ```
 var box = 0 / 0; // NaN
 var box = 12 / 0; // Infinity
 var box = 12 / 0 * 0; // NaN

 alert(Number.NaN); // NaN
 alert(NaN+1); // NaN
 alert(NaN == NaN) // false
 alert(NaN === NaN) // false
 ```

- `Number.isNaN()`函数，用来判断值是不是`NaN`

 ```
 alert(isNaN(NaN)); // true
 alert(isNaN(25)); // false，25 是一个数值
 alert(isNaN('25')); // false，'25'是一个字符串数值，可以转成数值
 alert(isNaN('Lee')); // true，'Lee'不能转换为数值
 alert(isNaN(true)); // false，true可以转成成1
 alert(isNaN(false)); // false，false可以转成成0
 ```

- 类型转换：`Number()`、`Number.parseInt()`和`Number.parseFloat()`。`Number()`函数是转型函数，可以用于任何数据类型，而另外两个则专门用于把字符串转成数值

 ```
 alert(Number(true)); // 1，Boolean 类型的true 和false 分别转换成1 和0
 alert(Number(25)); // 25，数值型直接返回
 alert(Number(null)); // 0，空对象返回0
 alert(Number(undefined)); // NaN，undefined 返回NaN

 // 字符串
 alert(Number('456')); // 456 整型
 alert(Number('070')); // 70 整型，去掉前面的0，如果这是八进制的数字转换后数值将会不正确
 alert(Number('08.90')); // 8.9 浮点数
 alert(Number('')); // 0 如果字符串是空，那么直接转换成0
 alert(Number('blabla') // NaN 如果是其它字符串类型，则返回NaN

 /* 如果是对象，首先会调用valueOf()方法，然后确定返回值是否能够转换成数值。
 如果转换的结果是NaN，则基于这个返回值再调用toString()方法，再测试返回值。*/
 var box = {
  toString : function () {
   return '123';
  }
 };
 alert(Number(box)); // 123
 ```
 ```
 // parseInt()从第一位解析到非整型数值位置。
 alert(parseInt('456Lee')); // 456，会返回整数部分
 alert(parseInt('Lee456Lee')); // NaN，如果第一个不是数值，就返回NaN
 alert(parseInt('12Lee56Lee')); // 12，从第一数值开始取，到最后一个连续数值结束
 alert(parseInt('56.12')); // 56，小数点不是数值，会被去掉
 alert(parseInt('')); // NaN，空返回NaN

 // ECMAScript为parseInt()提供了第二个参数，用于解决各种进制的转换。
 alert(parseInt('0xAF')); // 175，十六进制
 alert(parseInt('AF',16)); // 175，第二参数指定十六进制，可以去掉0x前缀
 alert(parseInt('AF')); // NaN，理所当然
 alert(parseInt('101010101',2)); // 341，二进制转换
 alert(parseInt('70',8)) // 56，八进制转换
 ```
 ```
 // parseFloat()是用于浮点数值转换的，和parseInt()一样，从第一位解析到非浮点数值位置。
 alert(parseFloat('123Lee')); // 123，去掉不是别的部分
 alert(parseFloat('0xA')); // 0，不认十六进制
 alert(parseFloat('123.4.5')); // 123.4，只认一个小数点
 alert(parseFloat('0123.400')); // 123.4，去掉前面的0
 alert(parseFloat('1.234e7')); // 12340000，把科学技术法转成普通数值
 ```

***

**String类型**

- 语法

 ```
 var str1 = 'string text';
 var str2 = "string text";
 var str3 = String("string text"); // 使用String()函数
 var str4 = new String("string text"); // 使用String对象来构造字符串
 ```

- 转义字符

 ```
 \n 换行
 \t 制表
 \b 空格
 \r 回车
 \f 换页
 \\ 斜杠
 \' 单引号
 \" 双引号
 ```

***

**Object类型**

- **通过构造函数创建对象**，语法`new Object( [ value ] )`，如果给定值是`null`或`undefined`，它生成并返回一个空对象，否则它将返回一个与给定值对应类型的对象

 ```
 // 定义空的Object对象
 var o1 = new Object();
 var o2 = new Object(undefined);
 var o3 = new Object(null);
 ```

- `JavaScript`语言的所有对象都是由`Object`衍生的对象；所有对象都继承了`Object.prototype`的方法和属性，尽管它们可能被覆盖。原型对象的更改会传播给所有的对象，除非这些属性和方法受到了原型链中那些进一步的变化的覆盖。

- 一个`JavaScript`对象有很多属性。一个对象的属性可以被解释称一个附加到对象上的一个变量。对象的属性和普通的`JavaScript`变量基本没什么区别，仅仅是属性属于某个对象。可以通过点符号来访问一个对象的属性

 ```
 objectName.propertyName
 ```

- 和其他`JavaScript`变量一样，对象的名字(可以是普通的变量)和属性的名字都是大小写敏感的。你可以在定义一个属性的时候就给它赋值。例如，我们创建一个`myCar`的对象然后给他三个属性，`make`，`model`，`year`。具体如下所示：

 ```
 var myCar = new Object();
 myCar.make = "Ford";
 myCar.model = "Mustang";
 myCar.year = 1969;
 ```

- `JavaScript`对象的属性也可以通过方括号访问。对象有时也被叫作关联数组，因为每个属性都有一个用于访问它的字符串值。例如，你可以按如下方式访问`myCar`对象的属性：

 ```
 myCar["make"] = "Ford";
 myCar["model"] = "Mustang";
 myCar["year"] = 1969;
 ```

- 一个对象的属性名可以是任何有效的`JavaScript`字符串，或者可以被转换为字符串的任何东西，包括空字符串。然而，一个属性的名称如果不是一个有效的`JavaScript`标识符（例如，一个有空格或短横线，或者以数字开头的属性名），就只能通过方括号标记访问。这个标记法在属性名称是动态判定（属性名只有到运行时才能判定）时非常有用。例如：

 ```
 var myObj = new Object(),
 str = "myString",
 rand = Math.random(),
 obj = new Object();

 myObj.type = "Dot syntax"; // type: "Dot syntax"
 myObj["date created"] = "String with space"; // date created: "String with space"
 myObj[str] = "String value"; // myString: "String value"
 myObj[rand] = "Random Number"; // 0.3309114803560078: "Random Number"
 myObj[obj] = "Object"; // [object Object]: "Object"
 myObj[""] = "Even an empty string"; // "": "Even an empty string"

 console.log(myObj);
 ```

- 除了通过构造函数创建对象之外，你也可以**通过对象初始化器创建对象**。使用对象初始化器也被称作通过字面值创建对象

 ```
var obj = { property_1:   value_1,   // property_# may be an identifier...
            2:            value_2,   // or a number...
            // ...,
            "property n": value_n }; // or a string
 ```

- 这里`obj`是新对象的名称，每一个`property_i`是一个标识符（可以是一个名称、数字或字符串字面量），并且每个`value_i`是一个其值将被赋予`property_i`的表达式。`obj` 与赋值是可选的；如果你不需要在其他地方引用对象，你就不需要将它赋给一个变量。（注意在接受一条语句的地方，你可能需要将对象字面量括在括号里，从而避免将字面量与块语句相混淆）

- 下例创建了有三个属性的`myHonda`对象。注意它的`engine`性也是一个拥有自己属性的对象。

 ```
 var myHonda = {color: "red", wheels: 4, engine: {cylinders: 4, size: 2.2}};
 ```

- **使用构造函数，通过两步来创建对象**
 - 通过创建一个构造函数来定义对象的类型。首字母大写是非常普遍而且很恰当的惯用法
 - 通过`new`创建对象实例

 ```
 // 注意通过使用 this 将传入函数的值赋给对象的属性
 function Car(make, model, year) {
   this.make = make;
   this.model = model;
   this.year = year;
 }

 var kenscar = new Car("Nissan", "300ZX", 1992);
 var vpgscar = new Car("Mazda", "Miata", 1990);
 ```

## 流程控制语句

[[Back To Top]](#jump-to-section)

**if...else**

- 语法

 ```
 if (condition)
   statement_1
 [else
   statement_2]

 if (condition)
   statement_1
 [else if (condition_2)
   statement_2]
 ...
 [else if (condition_n_1)
   statement_n_1]
 [else
   statement_n]

 if (condition) {
   statements_1
 } else {
   statements_2
 }
 ```

- 下面的值计算结果将为false；所有其它值，包括所有对象将为true
 - false
 - undefined
 - null
 - 0
 - NaN
 - the empty string ("")

***

**switch**

- 语法

 ```
 switch (expression) {
    case label_1:
       statements_1
       [break;]
    case label_2:
       statements_2
       [break;]
    ...
    default:
       statements_def
       [break;]
 }
 ```

***

**do...while**

- 先运行，后判断的循环语句。也就是说，不管条件是否满足，至少先运行一次循环体
- 语法

 ```
 do [{]
    statement
 [}] while (condition);
 ```

***

**while**

- 语法

 ```
 while (condition) [{]
    statement
 [}]
 ```

***

**for**

- 语法

 ```
 for ([initialExpression]; [condition]; [incrementExpression]) [{]
    statement
 [}]
 ```
 ```
 for (var i = 0; i < 10; i++) {
    console.log(i); // 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
 }
 ```

***

**for...in**

- 遍历对象的所有属性
- 语法

 ```
 for (variable in object) {
    statements
 }
 ```
 ```
 var sum = 0;
 var obj = {prop1: 5, prop2: 13, prop3: 8};
 for (var item in obj) {
   console.log(item); // prop1, prop2, prop3
   console.log(obj[item]); // 5, 13, 8
 }
 ```

***

**label**

- label值可以是任何JavaScript的标识符，不能是关键字、保留字
- 尽可能避免使用标签，因为它们使得程序难以阅读和理解
- 语法

 ```
 label :
    statement
 ```
 ```
 // In this example, the label markLoop identifies a while loop.
 // 在这个例子中，标签markLoop标识while循环
 markLoop:
 while (theMark == true) {
    doSomething();
 }
 ```

***

**break**

- 使用break语句来终止循环， switch ，或与一个标签语句一起
 - 当使用break没有标签，它会终止最内层的while，do-while，for，或switch立即将控制权转移到下面的语句
 - 当使用break一个标签，它会终止指定的标签代码块
- 语法
 - `break;`
 - `break label;`

 ```
 var i, j;

 loop1:
 for (i = 0; i < 3; i++) {      // 第一个for循环被标记为 "loop1"
    loop2:
    for (j = 0; j < 3; j++) {    // 第二个for循环被标记为 "loop2"
       if (i == 1 && j == 1) {
          break loop1;
       }
       console.log("i = " + i + ", j = " + j);
    }
 }

 // Output is:
 //   "i = 0, j = 0"
 //   "i = 0, j = 1"
 //   "i = 0, j = 2"
 //   "i = 1, j = 0"
 // 注意它如何跳过了以下输出：
 //   "i = 1, j = 1"
 //   "i = 1, j = 2"
 //   "i = 2, j = 0"
 //   "i = 2, j = 1"
 //   "i = 2, j = 2"
 ```

***

**continue**

- 在continue语句可用于重新启动while， do-while， for，或label语句
 - 当使用continue没有标签，它会终止最内层的当前迭代while， do-while还是for语句并继续执行下一个迭代循环。与此相反的break声明，continue不会终止整个循环的执行。 在while循环，它跳回条件。在for循环，它跳转到increment-expression
 - 当使用continue一个标签，它用于循环语句中的标签代码块
- 语法
 - `continue;`
 - `continue label;`

 ```
 var i, j;

 loop1:
 for (i = 0; i < 3; i++) {      // 第一个for循环被标记为 "loop1"
    loop2:
    for (j = 0; j < 3; j++) {    // 第二个for循环被标记为 "loop2"
       if (i == 1 && j == 1) {
          continue loop1;
       }
       console.log("i = " + i + ", j = " + j);
    }
 }

 // Output is:
 //   "i = 0, j = 0"
 //   "i = 0, j = 1"
 //   "i = 0, j = 2"
 //   "i = 1, j = 0"
 //   "i = 2, j = 0"
 //   "i = 2, j = 1"
 //   "i = 2, j = 2"
 // 注意它如何跳过了 "i = 1, j = 1" 和 "i = 1, j = 2"
 ```

***
