# 语法、关键字、保留字、数据类型

---
前言：最近在细读Javascript高级程序设计，对于我而言，中文版，书中很多地方一笔带过，所以用自己所理解的，尝试细致解读下。如有纰漏或错误，会非常感谢您的指出。文中绝大部分内容引用自《JavaScript高级程序设计第三版》。

---

任何语言的核心都必然会描述这门语言最基本的工作原理。
而描述的内容通常都要涉及这门语言的语法、操作符、数据类型、内置功能等用于构建复杂解决方案的基本概念。

## 语法

1. 区分大小写

ECMAScript中的一切（变量、函数和操作符）都区分大小写。
这也就意味着，变量名test和变量名Test是两个不同的变量，而函数名不能使用typeof，因为它是一个关键字，但typeOf则完全可以是一个有效的函数名。

2. 标识符

标识符，就是指变量、函数、属性的名字，或者函数的参数。

标识符可以是按照下列格式规则组合起来的一或多个字符：

- 第一个字符必须是一个字母、下划线（_）或一个美元符号（$）。
- 其他字符可以是字母、下划线、美元符号或数字。
  
按照惯例，ECMAScript标识符采用驼峰大小写格式，也就是第一个字母小写，剩下的每个单词的首字母大写。

```
firstSecond;
myCar;
doSomethingImportant;
```

虽然没有谁强制要求必须采用这种格式，**为了与ECMAScript内置的函数和对象命名格式保持一致，可以将其当做一种最佳实践。**

**不能把关键字、保留字、true、false和null用作标识符。**


3. 注释

ECMAScript使用C语言风格的注释，包括单行注释和块级注释。

单行注释以两个斜杠开头

```
//单行注释
```

块级注释以一个斜杠和一个星号开头，以一个星号和一个斜杠结尾。

```
/*
 *这是一个多行
 *注释
*/
```

虽然上面注释中的第二和第三行都以一个星号开头，但这不是必需的。之所以添加那两个星号，纯粹是为了提高注释的可读性（这种格式在企业级应用中用的比较多）。

4. 严格模式

ES5引入了严格模式（strict mode）的概念。

严格模式是为JavaScript定义了一种不同的解析与执行模型。

**在严格模式下，ES3中的一些不确定的行为将得到处理，而且对某些不安全的操作也会抛出错误。要在整个脚本中启用严格模式，可以在顶部添加如下代码。**

```
"use strict";
```

这行代码看起来像是字符串，而且也没有赋值给任何变量，但其实它是一个编译指示（pragma），用于告诉会吃的JavaScript引擎切换到严格模式。 **这是为不破坏ES3语法而特定的语法。**

在函数内部的上方包含这条编译指示，也可以指定函数在严格模式下运行。

```
function doSomething() {
    "use strict";
    //function body
}
```

**严格模式下，JavaScript的执行结果会有很大不同。**

5. 语句

ECMAScript中的语句以一个分号结尾；如果省略分号，则由解析器确定语句的结尾。

```
var sum = 1 + 2 //即使没有分号也是有效的语句-不推荐
var diff = 3 - 4; //有效的语句-推荐
```

虽然语句结尾的分号不是必须的，但建议任何时候都不要省略它。因为加上这个分号可以避免很多错误（例如不完整的输入），开发人员也可以放心地删除多余的空格来压缩ES代码。另外，加上代码也会在某些情况下增进代码的性能，这样解析器就不必花时间推测应该在哪里插入分号了。

**可以使用C语言风格把多余语句组合到一个代码块中，即代码块以左花括号（{）开头，以右花括号（}）结尾。**

```
if(test) {
    test = false;
    console.log(test);
}
```

虽然条件控制语句（如if语句）只在执行多条语句的情况下才要求使用代码块，但最好是始终在控制语句中使用代码块——即使代码块中只有一条语句。

```
if (test) console.log(test); //有效但容易出错，不推荐

if (test) {//推荐使用
    console.log(test); 
}
```

在控制语句中使用代码块可以让编码意图更加清晰，而且也能降低修改代码时出错的几率。

## 关键字和保留字

ES描述一组具有特定用途的关键字，这些关键字可用于表示控制语句的开始或结束，或者用于执行特定的操作。按照规则，关键字也是语言保留的，不能用做标识符。

ES5的关键字

```
if else do return

switch case break while do continue

finally void with debugger function this with

var typeof instanceof default delete in 

new try catch throw

```

ES-262定义的保留字

```
abstract enum int short

boolean export interface static

byte extends long super

char final native synchronized

class float package throws

const goto private transient

debugger implements protected volatile

double import public
```

在非严格模式下运行时的保留字缩减为下列这些：

```
class enum extends super

const export import
```

在严格模式下，第5版还对以下保留字施加限制：

```
implements package public

interface private static

let protected yied
```

let和yield是第5版新增的保留字；其他保留字都是第3版定义的。

第5版对使用关键字和保留字的规则进行了少许修改。关键字和保留字虽然仍然不能作为标识符使用，但现在可以用作对象的属性名。一般来说，最好不要使用关键字和保留字作为标识符和属性名，以便与将来的ECMAScript版本兼容。

ECMA-262第5版对eval和arguments施加了限制。
在严格模式下，这两个名字不能作为标识符或属性名，否则会抛出错误。

## 变量

ES的变量是松散类型的，所谓松散类型就是可以用来保存任何类型的数据。换句话说，每个变量仅仅是一个用于保存值的占位符而已。定义变量时要使用var操作符（注意var是一个关键字），后跟变量名（标识符）。

```
var message; //undefined
```

折行代码定义了一个名为message的变量，该变量可以用来保存任何值（像这样未经过初始化的变量，会保存一个特殊的值——undefined）。ES也支持直接初始化变量，因此在定义变量的同时就可以设置变量的值。

```
var message = "hi"
```

在此，变量message中保存了一个字符串值"hi"。像这样初始化变量并不会把它标记为**字符串类型。**初始化的过程就是给变量赋一个值那么简单。因此，可以在修改变量值的同时修改值的类型。

```
var message = "hi";
message = 100; //有效，但不推荐
```

**用var操作符定义的变量将成为定义该变量的作用域中的局部变量。也就是说，如果在函数中使用var定义一个变量，那么这个变量在函数退出后就会被销毁。**

```
function() {
    var message = "hi";
}
test();
console.log(message); //error, message is not defined.
```

变量message是在函数中使用var定义的。当函数被调用时，就会创建该变量并为其赋值。而在此之后，这个变量又会立即被销毁，因此下一行代码会导致错误。

不过，可以像下面这样省略var操作符，从而创建一个全局变量。

```
function test() {
    message = "hi";
}

test();

console.log(message);
```

这个例子省略了var操作符，因而message就成了全局变量。这样，只要调用过一次test()函数，这个变量就有了定义，就可以在函数外部的任何地方被访问到。

**虽然省略var操作符可以定义全局变量，这也不是我们推荐的做法。因为在局部作用域中定义的全局变量很难维护，而且如果有意地忽略了var操作符，也会由于相应变量马上就有定义而导致不必要的混乱。给未经声明的变量赋值在严格模式下抛出ReferenceError错误。**

可以使用一条语句定义多个变量。同样由于ECMAScript是松散类型的，因而使用不同类型初始化变量的操作可以放在一条语句中完成。虽然代码里的换行和变量缩进不是必需的，但这样做可以提高可读性。

在严格模式下，不能定义名为eval或arguments的变量，否则会导致语法错误。

## 数据类型

**ECMAScript中有5中简单数据类型（也成为基本数据类型）：String, Number, Boolean, Undefined, null。还有一种复杂数据类型——Object，Object本质上是由一组无序的名值对组成的。**

ECMAScript不支持任何创建自定义类型的机制，而所有值最终都是上述6种数据类型之一。

由于ECMAScript数据类型具有动态性，因此的确没有再定义其他数据类型的必要了。

