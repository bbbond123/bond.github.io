---
layout: post
title: JavaScript 数据类型总结
description: javascript数据类型有5中类型:undefined null boolean number string object
category: blog
---

## 数据类型
javascript数据类型有5中类型:`undefined` `null` `boolean` `number` `string` 
`object`object本质上是一组无序的名值对组成的。

## typeof操作符
介于JavasScript是松散类型的,因此需要有一种手段来检测给定变量的数据类型--typeof就是负责提供者方面信息的操作符。对一个使用typeof操作符可以返回下列某个字符串:

* `underfined` ——如果这个值未定义
* `boolean` ——如果这个值是布尔值
* `string` ——如果这个值是字符串
* `number` ——如果这个值是数值
* `object` ——如果这个值是对象或null
* `function` ——如果这个值是函数

## Undefined 类型
Undefined 类型只有一个值，即特殊的undefined。在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined,例如:

    var message;
    alert(message == undefined) //true


## Null类型
Null 类型是第二个只有一个值的数据类型，这个特殊的值就是null。从逻辑角度来看，null表示一个空对象指针，而这也正是使用typeof操作符检测null时会返回`object`的原因，例如:

    var car = null;
    alert(typeof car); // "object"

如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为null而不是其他值。这样一来，只要直接检测null值就可以知道相应的变量是否已经保存了一个对象的引用了，例如:

    if(car != null){
        //对car对象执行某些操作
    }


>实际上，undefined值是派生自null值的，因此`ECMA-262`规定对它们的相等性测试要返回true。

    alert(undefined == null); //true


尽管null和undefined有这样的关系，但它们的用途完全不同。无论在什么情况下都没有必要把一个变量的值显式地设置为undefined，可是同样的规则对null却不适用。换句话说，只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存null值。这样做不仅可以体现null作为空对象指针的惯例，而且也有助于进一步区分null和undefined。

类型
该类型只有两个字面值:true和false。这两个值与数字值不是一回事，因此true不一定等于1，而false也不一定等于0。
虽然Boolean类型的字面值只有两个，但JavaScript中所有类型的值都有与这两个Boolean值等价的值。要将一个值转换为其对应的Boolean值，可以调用类型转换函数Boolean()，例如:

    var message = 'Hello World';
    var messageAsBoolean = Boolean(message);

在这个例子中，字符串message被转换成了一个Boolean值，该值被保存在messageAsBoolean变量中。可以对任何数据类型的值调用Boolean()函数，而且总会返回一个Boolean值。至于返回的这个值是true还是false，取决于要转换值的数据类型及其实际值。下表给出了各种数据类型及其对象的转换规则。
![数据类型](http://bond.qiniudn.com/D8lg+hju628IAAAAAElFTkSuQmCC.png)

这些转换规则对理解流控制语句（如if语句）自动执行相应的Boolean转换非常重要，例如:
    
    var message = 'Hello World'; 
    if(message) 
    { 
    alert("Value is true"); 
    } 

运行这个示例，就会显示一个警告框，因为字符串message被自动转换成了对应的Boolean值（true）。由于存在这种自动执行的Boolean转换，因此确切地知道在流控制语句中使用的是什么变量至关重要。
## Number类型
这种类型用来表示整数和浮点数值，还有一种特殊的数值，即NaN（非数值 Not a Number）。这个数值用于表示一个本来要返回数值的操作数未返回数值的情况（这样就不会抛出错误了）。例如，在其他编程语言中，任何数值除以0都会导致错误，从而停止代码执行。但在JavaScript中，任何数值除以0会返回NaN，因此不会影响其他代码的执行。

　　NaN本身有两个非同寻常的特点。首先，任何涉及NaN的操作（例如NaN/10）都会返回NaN，这个特点在多步计算中有可能导致问题。其次，NaN与任何值都不相等，包括NaN本身。例如，下面的代码会返回false。
    alert(NaN == NaN);    //false

JavaScript中有一个isNaN()函数，这个函数接受一个参数，该参数可以使任何类型，而函数会帮我们确定这个参数是否“不是数值”。isNaN()在接收一个值之后，会尝试将这个值转换为数值。某些不是数值的值会直接转换为数值，例如字符串”10“或Boolean值。而任何不能被转换为数值的值都会导致这个函数返回true。例如:

    alert(isNaN(NaN));    //true
    alert(isNaN(10));    //false(10是一个数值)
    alert(isNaN("10"));    //false(可能被转换为数值10)
    alert(isNaN("blue"));    //true(不能被转换为数值)
    alert(isNaN(true));    //false(可能被转换为数值1)

有3个函数可以把非数值转换为数值：Number()、parseInt()和parseFloat()。第一个函数，即转型函数Number()可以用于任何数据类型，而另外两个函数则专门用于把字符串转换成数值。这3个函数对于同样的输入会返回不同的结果。
Number()函数的转换规则如下:

* 如果是Boolean值，true和false将分别被替换为1和0
* 如果是数字值，只是简单的传入和返回
* 如果是null值，返回0
* 如果是undefined，返回NaN
* 如果是字符串，遵循下列规则:
  * 如果字符串中只包含数字，则将其转换为十进制数值，即”1“会变成1，”123“会变成123，而”011“会变成11（前导的0被忽略） 
  * 如果字符串中包含有效的浮点格式，如”1.1“，则将其转换为对应的浮点数（同样，也会忽略前导0）
  * 如果字符串中包含有效的十六进制格式，例如”0xf“，则将其转换为相同大小的十进制整数值
  * 如果字符串是空的，则将其转换为0
  * 如果字符串中包含除了上述格式之外的字符，则将其转换为NaN 
* 如果是对象，则调用对象的valueOf()方法，然后依照前面的规则转换返回的值。如果转换的结果是NaN，则调用对象的toString()方法，然后再依次按照前面的规则转换返回的字符串值。

```
var num1 = Number("Hello World");    //NaN
var num2 = Number("");                //0
var num3 = Number("000011");        //11
var num4 = Number(true);            //1
```

由于Number()函数在转换字符串时比较复杂而且不够合理，因此在处理整数的时候更常用的是parseInt()函数。parseInt()函数在转换字符串时，更多的是看其是否符合数值模式。它会忽略字符串前面的空格，直至找到第一个非空格字符。如果第一个字符串不是数字字符或者负号，parseInt()会返回NaN；也就是说，用parseInt()转换空字符串会返回NaN。如果第一个字符是数字字符，praseInt()会继续解析第二个字符，知道解析完所有后续字符或者遇到了一个非数字字符。例如，"1234blue"会被转换为1234，”22.5“会被转换为22，因为小数点并不是有效的数字字符。

　　如果字符串中的第一个字符是数字字符，parseInt()也能够识别出各种整数格式（即十进制、八进制、十六进制）。为了更好的理解parseInt()函数的转换规则，下面给出一些例子

    var num1 = parseInt("1234blue");    //1234
    var num2 = parseInt("");            //NaN
    var num3 = parseInt("0xA");            //10（十六进制）
    var num4 = parseInt("22.5");        //22
    var num5 = parseInt("070");            //56（八进制）
    var num6 = parseInt("70");            //70
    var num7 = parseInt("10",2);        //2（按二进制解析）
    var num8 = parseInt("10",8);        //8(按八进制解析)
    var num9 = parseInt("10",10);        //10（按十进制解析）
    var num10 = parseInt("10",16);        //16（按十六进制解析）
    var num11 = parseInt("AF");            //56（八进制）
    var num12 = parseInt("AF",16);        //175

与parseInt()函数类似，parseFloat()也是从第一个字符（位置0）开始解析每个字符。而且也是一直解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止。也就是说，字符串中的第一个小数点是有效的，而第二个小数点就是无效的了，因此它后面的字符串将被忽略。例如，”22.34.5“将会被转换成22.34。

　　parseFloat()和parseInt()的第二个区别在于它始终都会忽略前导的零。由于parseFloat()值解析十进制值，因此它没有用第二个参数指定基数的用法。

    var num1 = parseFloat("1234blue");    //1234
    var num2 = parseFloat("0xA");        //0
    var num3 = parseFloat("22.5");        //22.5
    var num4 = parseFloat("22.34.5");    //22.34
    var num5 = parseFloat("0908.5");    //908.5

## String类型
String类型用于表示由零或多个16位Unicode字符组成的字符序列，即字符串。字符串可以由单引号(')或双引号(")表示。

    var str1 = "Hello";
    var str2 = 'Hello';

任何字符串的长度都可以通过访问其length属性取得

    alert(str1.length);        //输出5
要把一个值转换为一个字符串有两种方式。第一种是使用几乎每个值都有的toString()方法。

    var age = 11;
    var ageAsString = age.toString();    //字符串"11"
    var found = true;
    var foundAsString = found.toString();    //字符串"true"

数值、布尔值、对象和字符串值都有toString()方法。但null和undefined值没有这个方法。

　　多数情况下，调用toString()方法不必传递参数。但是，在调用数值的toString()方法时，可以传递一个参数：输出数值的基数。

    var num = 10;
    alert(num.toString());      //"10"
    alert(num.toString(2));     //"1010"
    alert(num.toString(8));     //"12"
    alert(num.toString(10));    //"10"
    alert(num.toString(16));    //"a"

通过这个例子可以看出，通过指定基数，toString()方法会改变输出的值。而数值10根据基数的不同，可以在输出时被转换为不同的数值格式。

　　在不知道要转换的值是不是null或undefined的情况下，还可以使用转型函数String()，这个函数能够将任何类型的值转换为字符串。String()函数遵循下列转换规则:

* 如果值有toString()方法，则调用该方法（没有参数）并返回相应的结果
* 如果值是null，则返回"null"
* 如果值是undefined，则返回”undefined“

```
    var value1 = 10;
    var value2 = true;
    var value3 = null;
    var value4;
    alert(String(value1));    //"10"
    alert(String(value2));    //"true"
    alert(String(value3));    //"null"
    alert(String(value4));    //"undefined"
```

## Object类型
对象其实就是一组数据和功能的集合。对象可以通过执行new操作符后跟要创建的对象类型的名称来创建。而创建Object类型的实例并为其添加属性和（或）方法，就可以创建自定义对象。

    var o = new Object();
Object的每个实例都具有下列属性和方法:

* constructor——保存着用于创建当前对象的函数
* hasOwnProperty(propertyName)——用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。其中，作为参数的属性名(propertyName)必须以字符串形式指定(例如：o.hasOwnProperty("name"))
* isPrototypeOf(object)——用于检查传入的对象是否是另一个对象的原型
* propertyIsEnumerable(propertyName)——用于检查给定的属性是否能够使用for-in语句来枚举
* toString()——返回对象的字符串表示
* valueOf()——返回对象的字符串、数值或布尔值表示。通常与toString()方法的返回值相同。