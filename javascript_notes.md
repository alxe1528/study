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

- 除了通过构造函数创建对象之外，你也可以**通过对象初始化器创建对象**。使用对象初始化器也被称作**通过字面值创建对象**

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

## 函数

[[Back To Top]](#jump-to-section)

**定义函数**

- 一个函数的定义（也称为函数的声明）由一系列的函数关键词组成，依次为：
 - 函数的名称
 - 函数的参数，包围在括号`()`中，并由逗号区隔的一个列表
 - 函数的`JavaScript`语句，包围在花括号`{}`中

 ```
 // 定义了一个名为square的简单函数
 function square(number) {
   return number * number;
 }
 ```

- 原始参数（比如一个具体的数字）被作为值传递给函数；值被传递给函数，但是如果被调用函数改变了这个参数的值，这样的改变不会影响到全局或调用的函数

- 如果你传递一个对象（即一个非实际值，例如矩阵或用户自定义的其它对象）作为参数，而函数改变了这个对象的属性，这样的改变对函数外部是可见的，如下面的例子所示

 ```
 function myFunc(theObject, theValue) {
   theObject.make = "Toyota";
   theValue = "hello";
 }

 var mycar = {make: "Honda", model: "Accord", year: 1998}, x, y;
 var z = "world";

 x = mycar.make;     // x gets the value "Honda"

 myFunc(mycar, z);
 y = mycar.make;     // y gets the value "Toyota"
                     // (the make property was changed by the function)
 console.log(z);     // z still gets the value "world"
 ```

- 请注意，重新给参数分配一个对象，并不会对函数的外部有任何影响，因为这样只是改变了参数的值，而不是改变了对象的一个属性值：

 ```
 function myFunc(theObject) {
   theObject = {make: "Ford", model: "Focus", year: 2006};
 }

 var mycar = {make: "Honda", model: "Accord", year: 1998}, x, y;

 x = mycar.make;     // x gets the value "Honda"

 myFunc(mycar);
 y = mycar.make;     // y still gets the value "Honda"
 ```

- 在第一段例子中，对象`mycar`被传递给了函数`myFunc`，进而函数改变了它。第二段例子里，函数并没有改变传递来的对象；相反，它生成了一个新的恰好和传递的全局对象同名的局部变量，因此对传递来的全局对象没有任何影响。

- 当然上述函数定义都用的是语法语句，函数也同样可以由**函数表达式**产生。这样的函数可以是**匿名**的；它不必有名称。例如，上面提到的函数`square`也可这样来定义：

 ```
 var square = function(number) {return number * number};
 ```

- 必要时，函数名称可与函数表达式同时存在，并且可以用于在函数内部代指其本身，或者在调试器堆栈跟踪中鉴别该函数：

 ```
 var factorial = function fac(n) {return n<2 ? 1 : n*fac(n-1)};
 console.log(factorial(3)); // output is: 6
 ```

- 函数表达式在将函数作为一个引数传递给其它函数时十分方便。下面的例子演示了一个叫`map`的函数如何被定义，而后调用一个匿名函数作为其第一个参数：

 ```
 function map(f,a) {
   var result = [], // Create a new Array
       i;
   for (i = 0; i != a.length; i++)
     result[i] = f(a[i]);
   return result;
 }

 console.log(map(function(x) {return x * x * x}, [0, 1, 2, 5, 10]));
 // output is: [0, 1, 8, 125, 1000]
 ```

***

**调用函数**

- 定义一个函数并不会自动的执行它。定义了函数仅仅是赋予函数以名称并明确函数被调用时该做些什么。调用函数才会以给定的参数真正执行这些动作。

- 函数一定要处于调用它们的域中，但是函数的声明可以在它们的调用语句之后，如下例：

 ```
 console.log(square(5));
 function square (n) {
   return n * n;
 }
 ```

- 函数的域是指函数被声明时的所在函数，或者函数在顶级被声明时指整个程序。注意只有使用如上的语法形式（即如`function funcName(){}`）才可以。而形如下面的代码是无效的。

 ```
console.log(square1(5)); // Uncaught ReferenceError: square1 is not defined
square1 = function (n) {
  return n * n;
}
 ```

- 函数可以被递归；就是说函数可以调用其本身。例如，下面这个函数计算递归的阶乘值：

 ```
 function factorial(n){
   if ((n == 0) || (n == 1))
     return 1;
   else
     return (n * factorial(n - 1));
 }

 var a, b, c, d, e;
 console.log(a = factorial(1)); // a gets the value 1
 console.log(b = factorial(2)); // b gets the value 2
 console.log(c = factorial(3)); // c gets the value 6
 console.log(d = factorial(4)); // d gets the value 24
 console.log(e = factorial(5)); // e gets the value 120

 square2 = function (n) {
    if ((n == 0) || (n == 1))
      return 1;
    else
      return (n * square2(n - 1));
 }
 console.log(square2(6)); // gets the value 720
 ```

***

**函数的域**

- 函数内定义的变量不能从函数之外的任何地方取得，因为变量仅仅在该函数的域的内部有定义。相反的，一个函数可以取得在它的域中定义的任何变量和子函数。换言之，定义在全局域中的函数可以取得所有定义在全局域中的变量。而定义在一个函数内部的子函数可以取得定义在其父函数内的，或已经由其父函数取得的任何变量。

 ```
 // The following variables are defined in the global scope
 var num1 = 20,
     num2 = 3,
     name = "Chamahk";

 // This function is defined in the global scope
 function multiply() {
   return num1 * num2;
 }

 console.log(multiply()); // Returns 60

 // A nested function example
 function getScore () {
   var num1 = 2,
       num2 = 3;

   function add() {
     return name + " scored " + (num1 + num2);
   }

   return add();
 }

 console.log(getScore()); // Returns "Chamahk scored 5"
 ```

***

**使用参数对象**

- 函数的参数会被保存在一个类似数组的对象中。在函数内，你可以按如下方式找出传入的引数：

 ```
 arguments[i]
 ```

- 其中`i`是参数的序号，以`0`开始。所以第一个传来的引参数会是`arguments[0]`。参数的全部数量由`arguments.length`表示。

- 使用参数对象，你可以用比它正式声明会接受的更多参数来调用函数。这在你事先不知道会需要将多少参数传递给函数时十分有用。你可以用`arguments.length`来决定传递给函数的参数的数量，然后用`arguments`对象来取得每个参数。

- 例如，设想有一个用来连接字符串的函数。唯一事先确定的参数，是在连接后的字符串中用来分隔各个连接部分的字符。

 ```
 function myConcat(separator) {
   var result = "", // initialize list
       i;
   // iterate through arguments
   for (i = 1; i < arguments.length; i++) {
      result += arguments[i] + separator;
   }
   return result;
 }

 // returns "red, orange, blue, "
 console.log(myConcat(", ", "red", "orange", "blue"));

 // returns "elephant; giraffe; lion; cheetah; "
 console.log(myConcat("; ", "elephant", "giraffe", "lion", "cheetah"));

 // returns "sage. basil. oregano. pepper. parsley. "
 console.log(myConcat(". ", "sage", "basil", "oregano", "pepper", "parsley"));
 ```

***

**预定义的函数**

`JavaScript`语言有好些个顶级的预定义函数：

- `eval()`
- `isFinite()`
- `isNaN()`
- `parseFloat()`
- `parseInt()`
- `decodeURI()`
- `decodeURIComponent()`
- `encodeURI()`
- `encodeURIComponent()`

## 内置核心对象

`JavaScript`语言中预定义的一些对象

- Array
- Boolean
- Date
- Function
- Math
- Number
- RegExp
- String

### Array Object

`JavaScript`语言其实并没有精确的数组数据类型，数组每个元素都可以保存任何数据类型

**创建数组**

- 通过`Array`对象来创建，或者数组字面量方式创建（又称为数组初始化器）

 ```
 var arr = new Array(element0, element1, ..., elementN);
 var arr = Array(element0, element1, ..., elementN);
 var arr = [element0, element1, ..., elementN];
 ```

- 若要创建一长度不为零但却不包含任何元素的数组，可以使用下列方式之一：

 ```
 var arr = new Array(arrayLength);
 var arr = Array(arrayLength);

 // This has exactly the same effect
 var arr = [];
 arr.length = arrayLength;
 ```

- **注意**：在上面的代码中，`arrayLength`必须是一个数值。否则将创建具有单一元素（为给定值）的数组。调用`arr.length`将返回`arrayLength`，但数组实际上包含空元素（`undefined`）。对数组使用`for...in`循环并不返回任何数组元素。

- 如果你需要将数组初始化包含唯一元素，并且这相元素恰好是单个数值，你必须使用方括号语法。当单个数值被传给构造函数或函数（取决于是否使用了`new`关键字）`Array()`时，它被解释为 `arrayLength`，而不是唯一元素。

 ```
 var arr = [42];
 var arr = Array(42); // Creates an array with no element, but with arr.length set to 42

 // The above code is equivalent to
 var arr = [];
 arr.length = 42;
 ```

- 对于`Array(N)`调用，若`N`是一个小数部分不为零的数值，则会得到`RangeError`。下面的例子说明了这个行为：

 ```
 var arr = Array(9.3);  // RangeError: Invalid array length
 ```

**数组赋值**

- 创建一个数组的同时填充它

 ```
 var myArray = new Array("Hello", myVar, 3.14159);
 var myArray = ["Mango", "Apple", "Orange"]
 ```

- 可以通过给元素赋值来填充数组

 ```
 var emp = [];
 emp[0] = "Casey Jones";
 emp[1] = "Phil Lesh";
 emp[2] = "August West";
 ```

- **注意**: 如果你在上面的代码中为数组操作符传递了一个非整型的值，则将为代表数组的对象创建一个属性，而不是一个数组元素：

 ```
 var arr = [];
 arr[3.4] = "Oranges";
 console.log(arr.length); // 0
 console.log(arr); // [3.4: "Oranges"]
 ```

**引用数组元素**

- 可以通过元素的索引来引用数组中的元素，元素的索引是从0开始的

 ```
 var myArray = ["Wind", "Rain", "Fire"];
 console.log(myArray[0]); // Wind
 console.log(myArray[1]); // Rain
 console.log(myArray[2]); // Fire
 ```

- **注意**: 数组操作符（方括号）也用于访问数组的属性（在`JavaScript`中数组也是一种对象）。例如：

 ```
 var arr = ["one", "two", "three"];
 arr["name"] = "Jerry";
 console.log(arr[2]); // three
 console.log(arr["length"]); // 3
 console.log(arr["name"]); // Jerry
 ```

**数组长度**

- 从实现角度`JavaScript`的数组将其元素作为普通的对象数组存储，并使用数组索引作为属性名`length`属性有些特别，它总是返回最后一个元素的索引再加上1。记着`JavaScript`的数组索引是从0而不1开始的。这意味着`length`属性总是比数组中最大的索引还要大1

 ```
 var cats = [];
 cats[30] = ['Dusty'];
 console.log(cats.length); // 31
 ```

- 你还可以给`length`属性赋值。写入一个比现有元素数小的值将截断数组，写入0将把数组全部清空：

 ```
 var cats = ['Dusty', 'Misty', 'Twiggy'];
 console.log(cats.length); // 3

 cats.length = 2;
 console.log(cats); // prints "Dusty,Misty" - Twiggy has been removed

 cats.length = 0;
 console.log(cats); // prints nothing; the cats array is empty

 cats.length = 3;
 console.log(cats[0]);  // undefined
 console.log(cats);  // [undefined, undefined, undefined] (maybe [] in chrome)
 ```

**遍历数组**

- 一个常见的操作是遍历数组的元素，并对每个元素进行处理。做这事最简单的方式如下：

 ```
 var colors = ['red', 'green', 'blue'];
 for (var i = 0; i < colors.length; i++) {
   console.log(colors[i]);
 }
 ```

- 如果你已知数组中的任何元素在条件上下文中都不会被计算成`false`——例如数组包含`DOM`元素——你可以使用一种更高效的惯用法：

 ```
 var divs = document.getElementsByTagName('div');
 for (var i = 0, div; div = divs[i]; i++) {
   /* Process div in some way */
 }
 ```

- 这避免了检查数组长度带来的开销，并且在每一次循环中更便捷地确保将当前项重新赋给变量`div`

- 在`JavaScript 1.6`中引入的`forEach()`方法，提供了另一种遍历数组的方法：

 ```
 var colors = ['red', 'green', 'blue'];
 colors.forEach(function(color) {
   console.log(color);
 });
 ```

- 传递给`forEach`的函数将针对每个元素执行一次，并且数组元素将作为参数传递给函数。未赋值的元素将不会在`forEach`循环中被遍历。

- **注意**：`forEach`的清单中不包括在数组定义时被省略的项目，但会包括被显式赋值为`undefined`的项目：

 ```
 var array = ['first', 'second', , 'fourth'];

 // returns ['first', 'second', 'fourth'];
 array.forEach(function(element) {
   console.log(element);
 })

 // true
 if(array[2] === undefined) {
   console.log('array[2] is undefined');
 }

 var array = ['first', 'second', undefined, 'fourth'];

 // returns ['first', 'second', undefined, 'fourth'];
 array.forEach(function(element) {
   console.log(element);
 })
 ```

- 因为`JavaScript`元素被作为标准的对象属性存储，所以不建议对数组使用`for...in`循环进行遍历，它导致普通的元素和所有可枚举的属性都会出现在清单中。

**数组的方法**

- `concat()` 将传入的数组或非数组值与原数组合并，组成一个新的数组并返回
  - `concat`方法将调用它的对象(`this`指向的对象)中的元素和若干个参数中的数组类型的参数中的元素以及非数组类型的参数本身按照顺序组合成一个新数组，并返回
  - `concat`方法并不修改调用它的对象(`this`指向的对象) 和参数中的各个数组本身的值，而是将它们的每个元素拷贝一份放在组合成的新数组中。原数组中的元素有两种被拷贝的方式：
    - 对象引用(非对象直接量)：`concat`方法会复制对象引用放到组合的新数组里，原数组和新数组中的对象引用都指向同一个实际的对象。所以，当实际的对象被修改时，两个数组也同时会被修改
    - 字符串和数字(是原始值，而不是包装原始值的`String`和`Number`对象)：`concat`方法会复制字符串和数字的值放到新数组里
  - 对新数组的任何操作都不会对原数组产生影响，反之亦然

 ```
 var myArray = new Array("1", "2", "3");
 myArray = myArray.concat("a", "b", "c");
 // myArray is now ["1", "2", "3", "a", "b", "c"]
 console.log(myArray);

 var alpha = ["a", "b", "c"];
 var numeric = [1, 2, 3];
 // 组成新数组 ["a", "b", "c", 1, 2, 3]; 原数组 alpha 和 numeric 未被修改
 var alphaNumeric = alpha.concat(numeric);
 console.log(alphaNumeric);

 var num1 = [1, 2, 3];
 var num2 = [4, 5, 6];
 var num3 = [7, 8, 9];
 // 组成新数组[1, 2, 3, 4, 5, 6, 7, 8, 9]; 原数组 num1, num2, num3 未被修改
 var nums = num1.concat(num2, num3);
 console.log(nums);

 var alpha = ['a', 'b', 'c'];
 // 组成新数组 ["a", "b", "c", 1, 2, 3], 原alpha数组未被修改
 var alphaNumeric = alpha.concat(1, [2, 3]);
 console.log(alphaNumeric);
 ```

- `join(separator)` 将数组的所有元素连接成一个字符串
  - `separator` 指定连接每个数组元素的分隔符，如果省略的话，默认为一个逗号`,`

 ```
 var a = new Array("Wind","Rain","Fire");
 var myVar1 = a.join();      // assigns "Wind,Rain,Fire" to myVar1
 var myVar2 = a.join(", ");  // assigns "Wind, Rain, Fire" to myVar2
 var myVar3 = a.join(" + "); // assigns "Wind + Rain + Fire" to myVar3
 ```

- `push(element1, ..., elementN)` 在数组的最后增加一个元素并且返回数组的新长度

 ```
 var myArray = new Array("1", "2");
 // output is: 3
 console.log(myArray.push("3")); // myArray is now ["1", "2", "3"]

 var sports = ["soccer", "baseball"];
 var total = sports.push("football", "swimming");
 console.log(sports); // ["soccer", "baseball", "football", "swimming"]
 console.log(total);  // 4
 ```

- `pop()` 从数组中删除最后一个元素并且返回该元素

 ```
 var myArray = new Array("1", "2", "3");
 var last = myArray.pop(); // myArray is now ["1", "2"], last = "3"
 console.log(last);
 ```

- `shift()` 从数组中删除第一个元素并且返回该元素

 ```
 var myArray = new Array ("1", "2", "3");
 var first = myArray.shift(); // myArray is now ["2", "3"], first is "1"
 console.log(first);
 ```

- `unshift(element1, ..., elementN)` 在数组开头增加一个或多个元素并且返回数组的新长度

 ```
 var myArray = new Array ("1", "2", "3");
 var total = myArray.unshift("4", "5"); // myArray becomes ["4", "5", "1", "2", "3"]
 console.log(myArray);
 console.log(total); // 5
 ```

- `slice(start_index, upto_index)` 抽取数组的一个片断并将其作为新数组返回

 ```
 var myArray = new Array ("a", "b", "c", "d", "e");
 var newArray = myArray.slice(1, 4); // starts at index 1 and extracts all elements until index 3
 console.log(newArray); // [ "b", "c", "d"]
 console.log(myArray); // ["a", "b", "c", "d", "e"]
 ```

- `splice(index, count_to_remove, addelement1, addelement2, ...)` 从数组中删除元素并且（可选地）替换它们

 ```
 var myArray = new Array ("1", "2", "3", "4", "5");
 myArray.splice(1, 3, "a", "b", "c", "d"); // myArray is now ["1", "a", "b", "c", "d", "5"]
 // This code started at index one (or where the "2" was), removed 3 elements there,
 // and then inserted all consecutive elements in its place.
 ```

- `reverse()` 将数组元素进行倒序：第一个的数组元素将变为最后一个，而最后的元素将变为第一个

 ```
 var myArray = new Array ("1", "2", "3");
 myArray.reverse(); // transposes the array so that myArray = [ "3", "2", "1" ]
 console.log(myArray);
 ```

- `sort()` 对数组元素进行排序
  - `sort()` 也可以接收一个函数用于判定元素的比较结果。该函数对两个值进行比较并且返回以下三个值之一：
    - 如果在排序方式中`a`小于`b`，则返回`-1`(或任何负数)
    - 如果在排序方式中`a`大于`b`，则返回`1 `(或任意正数)
    - 如果`a`和`b`相等，则返回`0`
  - `sort()` 对数字排序和字符串排序算法是一致的

 ```
 var myArray = new Array("Wind", "Rain", "Fire");
 myArray.sort(); // sorts the array so that myArrray = [ "Fire", "Rain", "Wind" ]
 console.log(myArray);

 function compare(a, b) {
   if (a < b)
      return -1;
   if (a > b)
      return 1;
   return 0;
 }
 var box = [0, 1, 5, 10, 15];
 box.sort(box)
 console.log(box); // [0, 1, 10, 15, 5]
 console.log(box.sort(compare)); // [0, 1, 5, 10, 15]
 ```

**以下方法在`JavaScript 1.6`引入**

- `indexOf(searchElement[, fromIndex])` 返回根据给定元素找到的第一个索引值，否则返回`-1`，搜索按升序索引顺序进行
  - `indexOf`使用strict equality（`===`）
  - `fromIndex` 该值为开始查找指定元素的索引值，默认值: `0`。如果该索引值大于或等于数组长度，则停止查找并返回`-1`。如果参数中提供的索引值是一个负值，则将其作为数组末尾的一个抵消，即-1表示从最后一个元素开始查找，`-2`表示从倒数第二个元素开始查找，以此类推。 **注意**：如果参数中提供的索引值是一个负值，仍然从前向后查询数组。如果抵消后的索引值仍小于`0`，则整个数组都将会被查询。

 ```
 var a = ['a', 'b', 'a', 'b', 'a'];
 console.log(a.indexOf('b')); // 1
 // Now try again, starting from after the last match
 console.log(a.indexOf('b', 2)); // 3
 console.log(a.indexOf('z')); // -1, because 'z' was not found
 ```

- `lastIndexOf(searchElement[, fromIndex])` 返回根据给定元素找到的第一个索引值，否则返回`-1`，搜索按降序索引顺序进行
  - `lastIndexOf`使用strict equality（`===`）
  - `fromIndex` 该值为开始查找指定元素的索引值，默认值: 数组的长度。如果`fromIndex`大于或等于数组长度，则搜索整个数组。如果`fromIndex`为负，则搜索从数组长度加上`fromIndex`的位置处开始。如果计算所得的索引小于`0`，则返回`-1`。

 ```
 var array = [2, 5, 9, 2];
 console.log(array.lastIndexOf(2)); // 3
 console.log(array.lastIndexOf(7)); // -1
 console.log(array.lastIndexOf(2, 3)); // 3
 console.log(array.lastIndexOf(2, 2)); // 0
 console.log(array.lastIndexOf(2, -2)); // 0
 console.log(array.lastIndexOf(2, -1)); // 3
 ```

- `forEach(callback[, thisArg])` 为每个数组元素执行一次指定的函数
  - `callback` 为每个数组元素执行的函数，`callback`函数会被依次传入三个参数：
    - 元素值
    - 元素索引
    - 被遍历的数组对象本身
  - `thisArg` 在执行`callback`函数时指定的`this`值
  - `forEach()` 遍历注意事项参考前面“遍历数组”的`forEach()`介绍

 ```
 function logArrayElements(element, index, array) {
     console.log("a[" + index + "] = " + element);
 }
 [2, 5, 9].forEach(logArrayElements);
 // logs:
 // a[0] = 2
 // a[1] = 5
 // a[2] = 9
 ```

- `map(callback[, thisArg])` 返回一个由原数组中的每个元素调用一个指定方法后的返回值组成的新数组
  - `callback` 原数组中的元素经过该方法后返回一个新的元素，`callback`函数会被依次传入三个参数：
    - 元素值
    - 元素索引
    - 被遍历的数组对象本身
  - `thisArg` 在执行`callback`函数时指定的`this`值
  - `map` 不修改调用它的原数组本身

 ```
 // Example: 将一个数组中的所有单词转换成对应的复数形式
 function fuzzyPlural(single) {
   var result = single.replace(/o/g, 'e');
   if( single === 'kangaroo'){
     result += 'se';
   }
   return result;
 }

 var words = ["foot", "goose", "moose", "kangaroo"];
 console.log(words.map(fuzzyPlural));
 // ["feet", "geese", "meese", "kangareese"]
 ```
 ```
 // 下面的语句返回什么呢:
 ["1", "2", "3"].map(parseInt);
 // 你可能觉的会是[1, 2, 3]
 // 但实际的结果是 [1, NaN, NaN]

 // 通常使用parseInt时,只需要传递一个参数.但实际上,parseInt可以有两个参数.第二个参数是进制数.可以通过语句"alert(parseInt.length)===2"来验证.
 // map方法在调用callback函数时,会给它传递三个参数:当前正在遍历的元素, 元素索引, 原数组本身.
 // 第三个参数parseInt会忽视, 但第二个参数不会,也就是说,parseInt把传过来的索引值当成进制数来使用.从而返回了NaN.

 //应该使用如下的用户函数returnInt
 function returnInt(element){
   return parseInt(element,10);
 }
 ["1", "2", "3"].map(returnInt);
 // 返回[1,2,3]
 ```

- `filter(callback[, thisArg])` 返回一个由原数组中的满足回调函数中指定条件的元素
  - `callback` 原数组中的元素经过该方法后返回`true/false`，`callback`函数会被依次传入三个参数：
    - 元素值
    - 元素索引
    - 被遍历的数组对象本身
  - `thisArg` 在执行`callback`函数时指定的`this`值
  - `filter` 不修改调用它的原数组本身

 ```
 function isBigEnough(element) {
   return element >= 10;
 }
 var filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
 console.log(filtered);
 // filtered is [12, 130, 44]
 ```

- `every(callback[, thisArg])` 确定数组的所有元素是否满足指定的测试，如果`callback`函数为所有数组元素返回`true`，则为`true`；否则为`false`。如果数组没有元素，则`every`方法将返回`true`
  - `callback` 原数组中的元素经过该方法后返回`true/false`，`callback`函数会被依次传入三个参数：
    - 元素值
    - 元素索引
    - 被遍历的数组对象本身
  - `thisArg` 在执行`callback`函数时指定的`this`值

 ```
 function isBigEnough(element, index, array) {
   return (element >= 10);
 }

 var passed = [12, 5, 8, 130, 44].every(isBigEnough);
 console.log(passed); // passed is false

 passed = [12, 54, 18, 130, 44].every(isBigEnough);
 console.log(passed); // passed is true

 passed = [].every(isBigEnough);
 console.log(passed); // passed is true
 ```

- `some(callback[, thisArg])` 确定数组的任何元素是否满足指定的测试，如果`callback`函数为任何数组元素返回`true`，则为`true`；否则为`false`。如果数组没有元素，则`some`方法将返回`false`
  - `callback` 原数组中的元素经过该方法后返回`true/false`，`callback`函数会被依次传入三个参数：
    - 元素值
    - 元素索引
    - 被遍历的数组对象本身
  - `thisArg` 在执行`callback`函数时指定的`this`值

 ```
 function isBigEnough(element, index, array) {
   return (element >= 10);
 }

 var passed = [2, 5, 8, 1, 4].some(isBigEnough);
 console.log(passed); // passed is false

 passed = [12, 5, 8, 1, 4].some(isBigEnough);
 console.log(passed); // passed is true

 passed = [5, 12, 8, 1, 4].some(isBigEnough);
 console.log(passed); // passed is true

 passed = [].some(isBigEnough);
 console.log(passed); // passed is false
 ```

 ***

 ### RegExp Object

 创建一个正则表达式对象，用特定的模式匹配文本

 **创建正则表达式**

 - `/pattern/flags` 使用字面量方式创建
   - `pattern` 正则表达式的文本
   - `flags` 该参数可以是下面几个值的任意组合
     - `g` 全局匹配
     - `i` 忽略大小写
     - `m` 让开始和结束锚点（`^`和`$`）工作在多行模式（也就是，`^`和`$`可以匹配字符串中每一行的开始和结束（行是由`\n`或`\r`分割的），而不只是整个输入字符串的最开始和最末尾处）

 ```
 var re = /ab+c/;
 var re = /ab+c/i;
 var re = /ab+c/igm;
 ```

- `RegExp(pattern [, flags])` 调用`RegExp`对象的构造函数

 ```
 var re = new RegExp("ab+c");
 var re = new RegExp("ab+c", "i");
 var re = new RegExp("ab+c", "igm");
 ```
- **注意**，字面量声明的参数无需引号，而函数声明的参数则需要放在引号里，以下是等价的：

 ```
 /ab+c/i;
 new RegExp("ab+c", "i");
 ```

**`RegExp`对象的属性**

- `global` 是否开启全局匹配，也就是匹配目标字符串中所有可能的匹配项，而不是只进行第一次匹配
- `ignoreCase` 在匹配字符串时是否要忽略字符的大小写
- `lastIndex` 下次匹配开始的字符串索引位置
- `multiline` 是否开启多行模式匹配（影响`^`和`$`锚点的行为）
- `source` 正则对象的源模式文本

**`RegExp`对象的方法**
- `exec` 在目标字符串中执行一次正则匹配操作，返回匹配的数组结果或者`null`
  - 如果`exec`方法没有找到匹配，将返回`null`。如果找到匹配项，则`exec`方法返回一个数组，并将更新全局`RegExp`对象的属性以反映匹配结果。数组元素`0`包含了完整的匹配项，而元素`1`到`n`包含的是匹配项中出现的任意一个子匹配项。这相当于没有设置全局标志 (`g`) 的`match`方法的行为
  - 如果为正则表达式设置了全局标志，则`exec`从`lastIndex`值指示的位置开始搜索字符串。如果没有设置全局标志，则`exec`忽略`lastIndex`的值，从字符串的起始位置开始搜索
  - `exec`方法返回的数组有三个属性：`input`、`index`和 `lastIndex`。`input` 属性包含整个被搜索的字符串。`index`属性包含了在整个被搜索字符串中匹配的子字符串的位置。`lastIndex`属性中包含了匹配中最后一个字符的下一个位置

 ```
 var text = "Образец text на русском языке";
 var regex = new RegExp("[\u0400-\u04FF]+", "g");

 var match = regex.exec(text);
 console.log(match[0]);  // prints "Образец"
 console.log(regex.lastIndex);  // prints "7"

 var match2 = regex.exec(text);
 console.log(match2[0]);  // prints "на" [did not print "text"]
 console.log(regex.lastIndex);  // prints "15"
 ```

 ```
 var text = "First line\nSecond line";
 var regex = /(\S+) line\n?/g;

 var match = regex.exec(text);
 console.log(match[1]);  // prints "First"
 console.log(regex.lastIndex); // prints 11

 var match2 = regex.exec(text);
 console.log(match2[1]); // prints "Second"
 console.log(regex.lastIndex); // prints "22"

 var match3 = regex.exec(text);
 console.log(match3 === null); // prints "true"
 ```

- `test` 测试当前正则是否能匹配目标字符串中的某一部分子字符串，返回`true/false`
  - `test` 方法检查字符串中是否存在某种模式，如果存在，则返回`true`，否则返回`false`
  - `test` 方法不修改全局`RegExp`对象的属性

 ```
 var text = "First line\nSecond line";
 var regex = /(\S+) line\n?/g;

 console.log(regex.test(text)); // prints "true"
 console.log(regex.lastIndex); // prints 11

 console.log(regex.test(text)); // prints "true"
 console.log(regex.lastIndex); // prints "22"

 console.log(regex.test(text)); // prints "false"
 ```

**`String`对象的正则表达式方法**

- `match(regexp)` 将字符串与正则表达式匹配，并返回一个包含该搜索结果的数组或者`null`
  - 如果`match`方法没有找到匹配，将返回`null`。如果找到匹配，则`match`方法返回一个数组，并将更新全局`RegExp`对象的属性以反映匹配结果
  - 如果没有设置全局标志 (`g`)，数组元素`0`包含整个匹配，而元素`1`到`n`包含任何一个子匹配。 此行为与未设置全局标志时`exec`方法（正则表达式）的行为相同。如果设置了全局标志，则元素`0`到元素`n`包含所有出现的匹配
  - 如果未设置全局标志，则`match`方法返回的数组有两个特性：`input`和`index`。`input`属性包含整个被搜索的字符串。`index`属性包含了在整个被搜索字符串中匹配的子字符串的位置
  - 如果设置了标志`i`，则搜索不区分大小写

 ```
 var src = "azcafAJAC";
 var re = /[a-c]/;
 var result = src.match(re);

 // The entire match is in array element 0.
 console.log(result[0] + "<br/>");

 // Now try the same match with the global flag.
 var reg = /[a-c]/g;
 result = src.match(reg);

 // The matches are in elements 0 through n.
 for (var index = 0; index < result.length; index++)
 {
     console.log ("submatch " + index + ": " +  result[index]);
 }
 // Output:
 // submatch 0: a demo.js:159
 // submatch 1: c demo.js:159
 // submatch 2: a
 ```

- `search(regexp)` 查找正则表达式搜索中第一个子字符串匹配项，返回匹配的索引或者`-1`

 ```
 var src = "is but a Dream within a dream";
 var re = /dream/;
 var pos = src.search(re);
 console.log(pos);
 // Output: 24

 re = /dream/i;
 pos = src.search(re);
 console.log(pos);
 // Output: 9
 ```

- `replace(regexp|substr, newSubStr|function)` 使用正则表达式，替换字符串
  - `regexp` 一个`RegExp`对象，该正则所匹配的内容会被第二个参数的返回值替换掉
  - `substr` 被替换掉的一个`String`
  - `newSubStr` 替换掉第一个参数在原字符串中的匹配部分，该字符串中可以内插一些特殊的变量名
  - `function` 回调函数。这个函数的返回值将作为最终`replace`匹配返回的新字符串。`replace`中的第一个参数（正则表达）`exec`匹配来的字符串将作为实参传递到这个函数

 ```
 // 使用字符串作为第二个参数
 // 替换字符串可以插入下面的特殊变量名
 $$  表示字符串 "$"
 $&  表示第一个参数所匹配的子串
 $`  位于匹配子串$&左边的内容
 $'  位于匹配子串$&右边的内容
 $n or $nn  如果n或nn是个十进制的数字，并且replace方法的第一个参数是个正则表达式，那么$n表示正则表达式中的第n个子匹配字符串
 ```

 ```
 // 替换 方法的所有实例替换“为“a.”
 var s = "the batter hit the ball with the bat";

 // Replace "the" with "a".
 var re = /the/g;
 var result = s.replace(re, "a");
 console.log(result);
 // Output: a batter hit a ball with a bat
 ```

 ```
 // replace 方法也可以替换模式中的子表达式。 下面的示例将字符串中的每对单词进行了交换：
 var s = "The quick brown fox jumped over the lazy dog.";
 var re = /(\S+)(\s+)(\S+)/g;
 // Exchange each pair of words.
 var result = s.replace(re, "$3$2$1");
 console.log(result);

 // Output: quick The fox brown over jumps lazy the dog.

 ```

 ```
 // 如何使用返回的函数替换文本，它转换为摄氏替换“F”后面的数字的任何实例
 // Initialize pattern.
 var test = /(\d+(\.\d*)?)F\b/g;
 var s1 = "Water freezes at 32F and boils at 212F.";

 // Use a function for the replacement.
 var s2 = s1.replace(test,
   function($0,$1,$2) {
     return((($1-32) * 5/9) + "C");
 });
 console.log(s2);
 // Output: Water freezes at 0C and boils at 100C.
 ```

 ***

