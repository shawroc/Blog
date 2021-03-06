# 内存回收 && 内存泄漏

---
前言：最近在细读Javascript高级程序设计，对于我而言，中文版，书中很多地方一笔带过，所以用自己所理解的，尝试细致解读下。如有纰漏或错误，会非常感谢您的指出。文中绝大部分内容引用自《JavaScript高级程序设计第三版》。

---

## 内存回收

在谈“内存泄漏”之前，首先，先了解下JavaScript的内存回收机制。

JavaScript具有内存自动回收机制，也就是说，执行环境会负责管理代码执行过程中使用的内存。

而在C和C++之类的语言中，开发人员的一项基本任务就是手动跟踪内存的使用情况，这是造成许多问题的根源。

**在编写JavaScript程序时，开发人员不用再关心内存使用问题，所需内存的分配以及所用内存的回收，完全实现了自动管理。**

**这种内存回收机制的原理，其实很简单。即：找出那些不再继续使用的变量，然后释放其占用的内存。**

**内存回收器会按照固定的时间间隔（或代码执行中预定的收集时间）， 周期性地执行这一操作。**


---

回顾下， 函数中局部变量的正常生命周期。

局部变量只在函数执行的过程中存在。而在这个过程中，会为局部变量在栈（或堆）内存上分配相应的空间，以便存储它们的值。

然后在函数中使用这些变量，直至函数执行结束。 

此时，局部变量就没有存在的必要了，因此可以释放它们的内存以供将来使用。

在这种情况下，很容易判断变量是否还有存在的必要了。

但是，实际情况却很复杂，不是那么容易得出结论的。

内存回收器必须跟踪哪个变量有用，哪个变量没用。

对于不再有用的变量打上标记，以备将来回收其占用的内存。

**用于标识无用变量的策略可能会因实现而异，具体到浏览器中的实现，则通常有两种策略。**

### 标记清除策略

JavaScript中最常用的内存回收方式是标记清除（mark-and-sweep)。当变量进入环境（例如：在函数中声明一个变量）时，就将这个变量标记为“进入环境”。

从逻辑上讲，永远不能释放进入执行环境的变量所占用的内存，只要执行流进入相应的环境，就可能会用到它们。

而当变量离开环境时，则将其标记为“离开环境”。

可以使用任何方式来标记变量。比如，可以通过翻转某个特殊的位来记录一个变量何时进入环境，或者使用一个“进入环境的”变量列表以及一个“离开环境的”变量列表，来跟踪变量。说到底，如何标记变量其实不重要，关键在于采取什么策略。

内存回收器在运行的时候会给存储在内存中的所有变量都加上标记（当然，可以使用任何标记方式）。
然后，它会去掉环境中正在引用的变量的标记（标记意味着要被回收）。
而后，再被加上标记的变量被视为准备回收，因为环境中的变量已经无法访问到这些变量了。
最后，内存回收器完成内存回收工作，销毁那些带标记的值，并回收它们所占用的内存空间。

IE、Firefox、Opera、Chrome和Safari的JavaScript内存回收，使用的都是标记清除氏的内存回收策略，只不过内存回收的时间间隔互有不同。


###  引用计数

**这一部分可稍作了解**

另一种不太常见的内存回收策略，**引用计数(reference counting)**。

引用计数的含义是跟踪记录每个值被引用的次数。

当声明了一个变量并将一个引用类型值赋给该变量时，则这个值的引用次数就是1。
如果同一个值又被赋给另外一个变量，则该值的引用次数加1。
相反，如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数减1。
当这个值的引用次数变成0时，则说明没有办法再访问这个值了，因而可以将其占用的内存空间回收。
当内存回收器再次运行时，它就会释放那些引用次数为零的值所占用的内存。

Netscape Navigator 3.0是最早使用引用计数策略的浏览器，但很快它就遇到一个严重的问题：循环引用。

**循环引用指的是对象A中包含一个指向对象B的指针，而对象B中也包含一个指向对象A的引用。**

```

function referenceCountingProblem () {
    //调用函数并执行的话
    var objectA = new Object(); // objectA引用值的reference counting 为1
    var objectB = new Object(); // objectB引用值的reference counting 为1 

    objectA.otherObject = objectB; // 现在objectB引用值的reference counting为2
    objectB.anotherObject = objectA; // 现在objectA引用值的reference counting为2

}

```

在这个例子中，objectA和objectB通过各自的属性相互引用；
这两个对象的引用次数都是2。

在采用标记清除策略的实现中，由于函数执行之后，这两个对象都离开了作用域，因此这种相互引用不是个问题。

但在采用引用计数策略的实现中，当函数执行完毕后，objectA和objectB还将继续存在，因为它们的引用次数永远不是0。
假如这个函数被重复多次调用，就会导致大量内存得不到回收。 为此，Netscape在Navigator4.0中放弃了引用计数策略，
转而采用标记清除（mark-and-sweep）来实现其内存回收机制。


可是，引用计数导致的麻烦并为就此终结。

IE中有一部分对象并不是原生JavaScript对象。 例如，BOM和DOM中的对象就是使用C++以COM对象（Component Object Model，组件对象模型）的形式实现的，而COM对象的内存回收机制采用的就是引用计数策略。

即使IE的JavaScript引擎是使用标记清除策略来实现的，但JavaScript访问的COM对象依然是基于引用计数策略的。
只要在IE中涉及COM对象，就会存在循环引用的问题。

```
var element = document.getElementById("some_element");
var myObject = new Object();
myObject.element = element; // 原生JS对象引用着DOM对象
element.someObject = myObject; // DOM对象引用着JS对象
```

以上代码，在一个DOM元素（element）和一个原生JavaScript对象（myObject）之间创建了循环引用。
其中，变量myObject有一个名为element的属性指向element对象，而变量element也有一个属性名叫someObject回指myObject。

由于存在这个循环引用，即使将例子中的DOM从页面中移出，它也永远不会回收。

为了避免这样的循环引用问题，最好是在不适用它们的时候手工断开原生JavaScript对象与DOM元素之间的连接。

```
myObject.element = null;
element.someObject = null;
```

将变量设置为null意味着切断变量与它此前引用的值之间的连接。当内存回收器再次运行时，就会删除这些值并回收它们占用的内存。

为了解决上述问题，IE9把BOM和DOM对象都转换成真正的JavaScript对象。
这样，就避免了两种内存回收算法并存导致的问题，也消除了常见的内存的泄漏问题。


### 内存泄漏

由于IE9之前的版本对JScript对象和COM对象使用不同的内存回收算法（策略）。

因此，闭包在IE的这些版本中会导致一些特殊的问题，具体来说，如果闭包的作用域链中保存着一个HTML元素，那么就意味着该元素无法被销毁。

```

function handler() {
    var element = document.getElementById("someElement");
    element.onclick = function() {
        alert(element.id);
    }
}

```

以上代码创建了一个座位element元素事件处理程序的闭包，而这个闭包则又创建了一个循环引用。
由于匿名函数保存了一个对hander()的活动对象的引用，因此就会导致无法减少element的引用数。
只要匿名函数存在，element的引用数至少也是1，因此，它所占用的内存就永远不会被回收。

不过，这个问题可通过稍微改写一下代码来解决。

```
function handler(){
    var element = document.getElementById("someElement");
    var id = element.id;

    element.onclick =  function(){
        console.log(id);
    };

    element = null;
}

```

在范例代码中，通过把element.id的一个副本保存在一个变量中，并且在闭包中引用该变量消除循环引用。
但仅仅做到这一步，还是不能解决内存泄漏的问题。
必须记住：闭包会引起包含函数的整个活动对象，而其中包含着element。
即使闭包不直接引用element，包含函数的活动对象中仍然会保存一个引用。
因此，有必要把element变量设置为null。
这样就能够解除对DOM对象的引用，顺利地减少其引用数，确保正常回收其占用的内存。

**关于这里的阐述，我有不同的看法。 既然闭包引用这个变量，说明这个变量，是我们需要用到的，某种意义上说，这不是“内存泄漏”！！**

### 内存回收导致的性能问题（IE）

**此部分也可稍作了解，当然知道这些历史，也会更加明白为啥都使用标记清除策略**

内存回收器是周期性运行的，如果为变量分配的内存数量很客观，那么回收工作量也是很大的。

在这种情况下，确定内存回收的时间间隔是一个非常重要的问题。

说到内存回收器多长时间运行一次，不禁让人联想到IE因此而声名狼藉的性能问题。

IE的内存回收器是根据内存分配量运行的，具体一点说就是256变量||4096个对象（或数组）字面量 和数组元素（slot）|| 64KB的字符窜。

达到上述任何一个临界值，内存回收器就会运行。

这种实现方式的问题在于，一个脚本中本来就包含那么多变量，那么该脚本很可能会在其生命周期中一直保有那么多的变量。

而这样一来，内存回收器，就不得不频繁的运行。 就引发了严重的性能问题。 促使IE7重写了其内存回收策略。

到IE7，其JavaScript引擎的内存回收的实现改变了方式：触发内存回收的变量分配、字面量或数组元素的临界值被调整为动态修正。

IE7中的各项临界值在初始时与IE6相等。如果内存回收过程中，回收的内存分配量低于15%，则变量、字面量或数组元素的临界值就会加倍。
这也说明，绝大多数变量是被引用着的，内存回收的临界值太低，需要往上调。

如果内存回收了85%的内尺寸分配量，则将各种临界值重置回默认值。

这一看似简单的调整，极大地提升了IE在运行包含大量JavaScript的页面时的性能。

事实上，在有的游览器红可以触发内存回收，但是不建议这么做。在IE中，调用window.CollectGarbage()方法会立即执行内存回收。在Opera7及更高版本中，调用window.opera.collect()也会启动内存回收。


## 管理内存

使用具备内存回收机制的语言编写程序，开发人员一般不必担心内存管理的问题。

但是，JavaScript在进行内存管理及内存回收面临的问题还是有点与众不同。

其中，最主要的一个问题，就是分配给Web浏览器的可用内存数量通常比分配给桌面应用程序的少。

这样做的目的是处于安全方面的考虑， 目的是防止运行JavaScript的网页耗尽全部系统内存而导致系统奔溃。

内存限制问题不仅会影响给变量分配内存，同时还会影响调用栈以及在一个线程中能够同时执行的语句数量。

**因此，确保占用最少的内存可以让页面获得更好的性能。优化内存占用的最佳方式，就是为执行中的代码只保存必要的数据。**

一旦数据不再有用，最好通过将其值设置为null来释放其引用——这个做法叫做接触引用（dereferencing）。

这一做法适用于大多数全局变量和全局对象的属性。

局部变量会在它们离开执行环境时自动被解除引用。

```

function createPerson(name) {
    var localPerson = new object();
    localPerson.name = name;
    return localPersonl;
}

var globalPerson = createPerson("Shaw");

//手工解除globalPerson的引用

globalPerson = null;

```

变量globalPerson取得了createPerson()函数返回的值。
在createPerson()函数内部，我们创建了一个对象并将其赋给局部变量localPerson，然后又为该对象添加了一个名为name的属性。
最后，当调用这个函数时，localPerson以函数值的形式返回并赋给全局变量globalPerson。
由于localPerson在createPerson()函数执行完毕后就离开了其执行环境，因此，无需我们显式地为它解除引用。

但是对于全局变量globalPerson而言，则需要我们在不使用它的时候手工为它解除引用，这也是上面例子中，最后一行代码的意义。

解除一个值的引用并不意味着自动回收该值所占用的内存。

解除引用的真正作用是让值脱离执行环境，以便内存回收器下次运行时将其回收。