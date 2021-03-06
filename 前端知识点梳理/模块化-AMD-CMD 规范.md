# 模块化-AMD-CMD 规范

## 为什么要使用模块化？

### 首先，何为模块化？

“模块”是为完成某一功能所需的一段程序或子程序。
模块是系统中“职责单一”且“可替换”的部分。

所谓的模块化就是指把系统代码分为一系列职责单一且可替换的模块。

模块化开发是指如何开发新的模块和复用已有的模块来实现应用的功能。

### 何为按需加载？

按需加载需要从时间和空间两方面理解。

空间上：只加载当前页面的模块。

时间上：只有当用户表现出需要某一功能的意图时，才去加载相关模块。

### 模块化开发与按需加载的适用场景

满足如下条件的应用适合采用模块化开发与按需加载技术：

- 应用复杂。不止一个功能部分，这些部分可能共享一些底层代码。

- 需要长期维护。开发初期可能需求不太明确，需要不断迭代开发，经常面临需求变更和功能添加。

- 对功能要求苛刻。面临复杂的交互和数据展现问题。


### 传统的js开发模式和加载模式是怎么样的？

在过去由于应用的复杂度不高，js 之于 web页面一直处于一种辅助程序的地位，甚至谈不上一门应用开发语言。而且多数网站都是一次性应用，规模较小，相对于可维护性，开发速度更重要。与其重构一个现有应用，还不如重写一个，在这样的环境下，采用传统的面向过程的编程模式足以应付开发需要。

由于网站规模小，与其把代码划分为小的模块，然后在不同的页面分别加载，还不如把相关的代码都几种写在一处，比如写一个common.js或share.js，然后所有的页面都引用这个文件。这样做开发简单，而且浏览器有缓存，首次加载后，后续无需网络传输，性能上不会有什么太大的问题。

### 传统开发模式的问题

- 由于代码的组织的结构是非模块化的，所以代码无法复用，进而导致代码重复，这就维护埋下了隐患。需求一旦变更，将导致代码多处更改，而随着应用规模的增大，代码将迅速进入难以维护的状态。

- 由于代码粒度太大，页面可能会加载大量根本用不到的代码，即便忽略网络传输的问题，过多无用代码，也会导致页面解析缓慢。

-由于所有代码都混在一起，无法有效测试，也就无法获得保证代码质量的有效手段。

### 回到正题？为什么需要模块化开发与按需加载

#### 解决变量命名冲突

#### 可维护性的需要

代码的可维护性的一种理解是，新功能的添加无需修改已有代码，旧有功能的变更无需修改多处代码。

对于初期需求不明确，需要采用不断迭代开发的项目，代码可维护性就显的尤为重要。

#### 可测性的需要

代码可测性的一种理解是，代码可以在系统环境外进行独立正确性验证。在系统环境外对代码进行测试十分重要，这不仅能保证代码的正确性，同时也保证了代码可以在不同环境中复用。

#### 性能的需要

模块化的代码可以实现按需加载，进而保证了不会把宝贵的页面加载时间浪费在下载和解析多余的代码上。

#### 架构的需求

架构的任务之一是保证系统可以应对未来的变化。
这些变化包跨新功能的添加，原有功能的修改，底层库文件的更换（如jQuery），性能优化等等。任何可以实现这一目标的架构都要求代码必须是模块化的。

#### 代码复用

代码复用不仅仅是为了节省开发时间，同时也是保证代码质量的有效手段，代码的复用程度越高，其质量就越容易得到保证。

#### 多人协作的需要

大型应用无法通过一人之力完成，多人协作是不可避免的。
在多人协作的环境下，经常要面临修改或使用别人写的代码的问题。
只有那些功能单一，接口明确，模块化代码我们才敢放心大胆的修改或使用。

### 模块化开发的理论基础

模块化开发时任何大型应用都必须采用的开发模式，同其他应用程序的开发一样，要实现js模块化开发，需要了解下面的理论基础。

- 面向对象

相对于面向过程式的编程模式，面向对象倡导的是以更符合现实世界的认知模式去构建我们的程序，而不是从计算机的角度去理解问题模型。其核心思想是“封装”，“继承”，“多态”。对于js模块化开发，“封装”的思想最为重要。**“封装”是指把代码的逻辑、方法或属性隐藏在对象（模块）内部。对外只提供必要的接口。**进而保证了代码的高内聚与低耦合。JavaScript不是一门纯粹的面向对象语言，它融合了面向过程，面向对象，函数式程序设计语言的思想，这也导致了这门语言的复杂性。为了更好的理解JavaScript面向对象编程思想推荐阅读以下两本书：《JavaScript语言精粹》，《JavaScript面向对象》。

- 设计模式

设计模式要解决的问题是如何组织和协调不同对象去解决问题。

- 单例模式。单例模式是指在程序运行期间保证一个类只有一个实例。应用单例模式其实就是保证我们的程序在运行期间，某一功能对象一直只是同一个对象，而不是每次都重复构建。

- 订阅者模式。这是JavaScript中应用最为广泛的模式。我们通过addEventListener或attachEvent为dom节点添加事件监听，其实就是在应用订阅者模式。**订阅者模式通过让一组对象去监听一个对象的事件，实现对象间一对多的通信，在最大程度上降低了对象间的耦合。**

- 外观模式。外观模式通过将一个或一组对象的接口封装起来，对外只提供其他代码需要的接口，实现降低代码耦合度的任务。


## 如何实践？

- CommonJS。JavaScript没有内建的模块支持，而CommonJS规范给出了完整的JavaScript实现模块的方式。

- 前端支持，有大量成熟的js按需就在框架可以使用。

- 后端支持，模块化的代码上线前需要进行打包压缩，打包过程需要通过源码进行静态分析来获得模块间的依赖关系，进而将相关模块打包在一起。

现在很流行的webpack，就是这一实践的最佳利器。


# CMD、AMD、CommonJS 规范分别指什么？有哪些应用？

CommonJS是用在服务器端的，同步的，如nodeJS。
AMD、CMD是用在浏览器端的，异步的，如requireJS和seaJS。

其中，AMD先提出，CMD是根据CommonJS和AMD基础上提出的。

## CommonJS规范

CommonJS 是服务器端模块的规范，Node.js采用了这个规范。

根据CommonJS规范，一个单独的文件就是一个模块。
加载模块使用require方法，该方法读取一个文件并执行，最后返回文件内部的exports对象。

```
//file -> foobar.js

//private variable
var test = 123;

//private method
function foobar(){
    this.foo = function(){
        //do something ....
    }
    this.bar = function(){
        //do something ....
    }
}

//exports对象上的方法和变量是公有的
var foobar = new foobar();

exports.foobar = foobar;

//require()方法默认读取js文件，所以可以省略js后缀
var test = require('./foobar').foobar;

test.bar();
```

CommonJS 加载模块是同步的，所以只有加载完成才能执行后面的操作。nodeJS主要用于服务器的编程，加载的模块文件一般都已经存在本地硬盘，所以加载起来比较快，不需要考虑异步加载的方式，所以CommonJS规范比较适用。但如果是浏览器环境，要从服务器加载模块，就必须采用异步模式，所以就有了AMD CMD 解决方案。

## AMD规范

AMD(Asynchronous Module Definition)

AMD 是 RequireJS 在推广过程中对模块定义的规范化产生。

AMD异步加载模块。它的模块支持对象、函数、构造器、字符串 JSON等各种类似的模块。

AMD规范使用define方法定义模块。

```
//通过数组引入依赖，回调函数通过形参传入依赖，依赖注入
define(['somemodule1', 'someModule2'], function(someModule1, someModule2) {
    
    function foo() {
        //something
        someModule1.test()
    }

    return {foo: foo}

});
```

AMD规范允许输出模块兼容CommonJS规范，这时define方法如下：

```
define(function(require, exports, modules) {
    var reqModule = require("./someModule");
    reqModule.test();

    modules.exports = reqModile.test();
})
```

## CMD

CMD即Common Module Definition, 通用模块定义。

CMD和AMD的区别有以下几点:

- CMD推崇依赖就近，AMD推崇依赖前置。

```
//AMD
define(['./a', './b'], function(a,b){
    //依赖一开始就写好
    a.test();
    b.test();
});

//CMD
define(function(require, exports, modules){
    //依赖可以就近书写
    var a = require('./a');
    a.test();

    //软依赖
    if(conditionIsTrue){
        var b = require('./b');
        b.test();
    }
});
```










