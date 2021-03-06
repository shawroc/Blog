# 实现响应式Web设计

---
绝大部分引用自《响应式Web设计 HTML5和CSS3实战（第2版）
---

在我最喜欢的故事和电影里，通常都会有这样一幕：导师给英雄一个建议或者赠予魔法物品。

你知道那些东西在日后会大有用处，只是你不知道什么时候以什么方式发挥作用。

好吧，我想在这最后一章中扮演一下导师的角色，另外，我的头发越来越少了，我看起来也不像英雄。我希望你，我的好徒弟，在你开始响应式设计前给我一点时间为你提点建议。

## 尽快让设计在浏览器和真实设备上运行起来

响应式Web设计做得越多，我越觉得尽快让设计在浏览器环境中运行起来很重要的。
如果你既是设计师又是开发者，这很简单。

只要你足够的灵感，就可以迅速地浏览器上开发出原型，然后再进行完善。

完全放弃高保真的整页实物模型，可以让我们更好地接受这种做法。

不过，也可以考虑一下Style Tiles——一个定位在情绪版(moodboard)和完整模型之间的产品。

Style Tiles的[介绍](http://styletil.es/)中是这样说的：

“Style Tiles是由字体、颜色、界面元素所组成的设计产品，用于展示Web页面中的视觉设计效果。”

我认为这能在相关人员间更好地展示和传递视觉设计的宗旨，而且再也不需要拼凑各种情绪板。

**让设计决定断点**

我想重申一下前几章中提到的一个点。
让设计决定断点。相比于在开发过程中决定断点，这更为容易一点。
你应当总是从最小的屏幕尺寸开始设计，渐渐地使视口尺寸增大，这样你就能知道在哪个地方加入断点。

你还会发现，这时候编码比较轻松。
你首先为最小的视口编写CSS，然后在媒体查询中修改其在较大视口下的表现。

```
.rule {
    /* 小型视口样式 */
}

@media (min-width: 40em) {
    .rule {
        /* 中型视口样式 */
    }
}

@media (min-width: 70em) {
    .rule {
        /* 大型视口样式 */
    }
}
```

## 在真实设备上观察和使用设计

如果可以，那就通过早期的设备（电话/平板电脑）来打造你自己的“设备实验室”吧。
具有多个不同设备是十分有帮助的。
这不仅能让你感觉到设计在不同设备上的表现，而且能在早期就暴露出一些布局、渲染问题。毕竟没人喜欢在已经完成一个项目后被告知在某些环境下代码无法正常工作。

**早测试，常测试！这并不需要花费太多。**

举个例子，你可以在ebay上购买二手的电话或者平板设备，或者从更新换代了设备的亲朋好友手中买入。

```
使用像BroswerSync这样的工具来同步你的工作

我近来使用过的一个最省时间的工具就是BrowserSync。
配置完成后，当你保存你的工作时，诸如CSS等的变化就会被注入到浏览器，而无需你不断地刷新屏幕。

如果这还不够吸引你，它还能通过WIFI将在不同设备上的浏览器刷新。

这节省了拿起每个测试设备点击刷新的时间。

它甚至能同步滚动和点击。

强烈推荐https://browsersync.io/。
```

## 拥抱渐进增强

在前面，我们简要介绍过渐进增强的概念。

这是一种我在实践中发现十分有用而且值得大力推广的开发方法。

**逐步增强的基本想法是，从选择支持的浏览器中选取它们共有的子集来开始编写你的前端代码（HTML、CSS、JavaScript)。然后，逐步优化你的代码以适应那些比较强大的浏览器和设备。**

这种方法看起来十分简单，事实上也确实如此，但如果你习惯了从最佳设备上开始设计，然后再降级你的代码，让它们能够在低版本的浏览器或者旧式设备上运行，你会发现渐进增强更为方便。

想象一下，你眼前是一个糟糕透了、老掉牙的设备，不能运行JavaScript，不支持Flexbox，不支持CSS3/CSS4。

在这种情况下，你可以做什么来提供一个不错的体验呢？

最重要的是，你应该编写能够精确描述你的内容的HTML5标记。
如果您正在构建的是一个基于文本和内容的网站，这个任务并不困难。

这种情况下，应专注于正确使用main、header、footer、article、section和aside等元素。

它不仅能让你的代码分成若干有效的部分，也能为你的用户提供更大的方便。

如果你正在构建Web应用或者图形化UI组件(跑马灯、标签卡、手风琴等)，则需要思考一下如何提炼有效的标记。

好的标记如此重要，是因为它为所有用户体验打下了良好的基础。你在HTML上的优化越多，你在CSS和JavaScript上为老式浏览器所做的优化就越少。

并且，没有人，真的没有人喜欢写代码来支持老式浏览器。

```
如果想要更好地了解渐进增强并且观看一些真实的例子，我推荐以下两篇文章。
它们深入介绍了如何使用HTML和CSS来实现一些复杂的交互。

https://www.cssmojo.com/how-to-style-a-carousel/

https://www.cssmojo.com/use-radio-buttons-for-single-option/
```

开始使用这种方式去开发并不是一件容易的事。
然而，这种开发能够大大地减轻你在低级浏览器上的工作量。

## 确定需要支持的浏览器

了解一个Web项目需要支持的浏览器和设备对于开发一个成功的响应式网站是十分重要的。我们已经了解了为什么渐进增强对于此十分有用。

如果你做的足够好，那么网站的绝大部分即使在最老的浏览器上也能有效运行。

但是，有的时候根据项目需要，你要从更为高级的浏览器开始编写。
例如，在你的项目中JavaScript是必需的，这种情况并不罕见。

在这种情况下，你仍然可以使用渐进增强的开发模式，只是你的起点不一样而已。

无论你的起点是什么，关键是建立它。

只有这时，你才能定义你想支持的不同浏览器和设备的视觉效果和功能体验。

### 等价的功能，而不是等价的外观

让网站在每个浏览器上的外观和工作方式一样是不现实也是不可取的。
除了某些浏览器专有怪癖，也需要考虑必要的功能问题。

例如，对于没有鼠标配置的触摸屏设备，我们就要考虑按钮和链接的触摸性。

**因此，作为一名Web开发人员，你应该告诉你的需求方（老板、客户、股东），“支持老式浏览器”并不意味着“在老式浏览器上看起来一模一样”。**

**我倾向于在支持的各个浏览器上功能一致而非外观一致。**
这意味着如果你要实现一个结账功能，所有用户都应该能够结账并且购买货物。

可能在现代浏览器上，用户可以体验更棒的视觉和交互效果，但是核心任务正在所有浏览器上都是可实现的。

### 选择要支持的浏览器

通常，当谈到要支持哪些浏览器的时候，我们其实是在讨论我们所支持的最古老的浏览器是什么。这里有几个可能性需要考虑，视情况而定。

如果已经是一个现有的王炸 ，那么看一下访客统计（Goole统计或者类似的方法）。

通过数字你可以做一些粗略的计算。

**例如，假如支持X浏览器的成本小于X浏览器将带来的价值，那么支持X浏览器。**

同样，加入观察到某个浏览器的用户统计持续低于10%，回顾过去并考虑未来发展趋势。在过去的3、6、12个月里，这个数据是怎么变化的？如果现在是6%，而且在过去的12个月里这个数据已经收缩一半，那么你就有强有力的理由放弃支持该款浏览器。

如果这是个新项目，并且没有统计数据，我通常会遵循“前两个版本” 策略，即是指当前的浏览器版本和之前的两个浏览器版本。

举个例子，如果IE12是目前的浏览器版本，那么你就要兼容IE10和IE11（前两个版本）。

这种选择是和那些“常青树”浏览器挂钩的，“常青树”浏览器是指那些以较短的周期持续更新版本的浏览器（如Firefox和Chrome）。

## 分层的用户体验

此时，让我们假设股东对Web开发有一定的了解，并且在团队中。
我们也假设你已经确定好了目标浏览器。

那么我们现在可以将体验分为不同层级。
我喜欢简单，所以会将它们区分为“基本”体验 和 “增强” 体验。

**基本体验是站点的最小可行版本，而增强体验则是包括所有功能并且最为美观的版本。**

当然，在你的层次里，可能要包括更多粒度。

例如，不同浏览器应该根据相应的特征提供不同的体验，比如是否支持Flexbox或者translate3d。

不管层次如何定义，你一定要定义它们，并且要知道你需要交付什么层次。

然后你就可以编写那些层次了。

**实现体验分层**

当前，Modernizr为基于浏览器兼容性的优化提供了最为稳健的方式。
尽管这意味着要为你的项目添加JavaScript依赖，但我认为这是值得的。

记住，当编写CSS的时候，没有被媒体查询包裹的代码或者没有被Modernizr添加选择器的代码，应该是由“基础”版本代码组成的。

然后通过Modernizr，我们可以根据浏览器的兼容性优化体验。

## 将CSS 断点 与 JavaScript 联系起来

通常，一些页面上的交互都会涉及JavaScript。
当你在开发响应式项目的时候，可能想在不同尺寸的视口里看到不同的效果。这也包括CSS也包括JavaScript。

假设我们想在到达某个CSS断点的时候调用特定的JavaScript函数。

**记住，“断点”是用来定义在响应式设计中某个显著改变点的术语）。**

让我们假设这个断点是47.5rem（如果字体大小是16像素，则这个断点是760像素），而我们只想在这个大小上运行函数。

最容易想到的方法就是量屏幕的尺寸，当尺寸值匹配的时候调用相应的函数。

JavaScript总是返回宽度的像素值而不是REM值，所以这里是第一个需要改变的地方。
然而，即使我们在CSS上将断点的值设置为像素值，这仍然意味着我们有两个地方需要维护。

万幸的是，我们有更好的方法。

我最先是Jeremy Keith的网站上看到这种[方法](https://adactio.com/journal/5429/)的。

基本思想是，我们在CSS上插入一些能够让JavaScript轻易理解的值。

看一下下面的CSS代码：

```
@media (min-width: 20rem) {
    body::after {
        content: "Splus";
        font-size: 0;
    }
}

@media (min-width: 47.5rem) {
    body::after {
        content: "Mplus";
        font-size: 0;
    }
}

@media (min-width: 62.5rem) {
    body::after {
        content: "Lplus";
        font-size: 0; 
    }
}
```

在每一个我们想和JavaScript沟通的断点处，我们使用了after伪元素（你可以使用before伪元素），并且将其内容设置为断点的名称。

在上例中，我使用了Splus对应小屏幕，Mplus对应中等大小屏幕，Lplus对应大屏幕。

你可以使用任何你认为合理的名字和值（不同的方位、不同的高度、不同的高度等）。

```
::before 和 ::after 伪元素是作为影子 DOM 元素插入到DOM中的。

::before作为第一个子元素插入，而::after则作为最后一个子元素插入。

你可以在你的浏览器的开发者工具中确认这一点。
```

在CSS设置中，我们可以看到DOM，并且能看到::after伪元素。

然后在JavaScript中，我们可以阅读这个值。

首先，我们将这个值赋给一个变量。

```
var size = window.getComputedStyle(document.body, ':after').getPropertyValue('content');
```

一旦获得了它，我们就可以做很多事情了。
为了证明这个概念，我编写了一个简单的自我调用函数（自我调用意味着它在浏览器解析它的时候马上被调用）来根据视口大小弹出不同的信息：

```
;funciton alertSize() {
    if(size.indexOf("Splus") != -1) {
        alert('I will run functions for small screens');
    } 
    
    if(size.indexOf("Mplus") != -1) {
        alert('At medium sizes, a different function could run');
    }

    if(size.indexOf("Lplus") != -1) {
        alert('Large screen here, different functions if needed');
    }
}();
```

我希望你可以在你的项目中做比弹出信息更为有趣的事情，我相信你会通过这种方式获益的。

这样，你也不会再遇到CSS媒体查询结果和JavaScript函数运行结果不一致的情况。

## 避免在生产中使用 CSS 框架

有很多免费的CSS框架旨在帮助快速搭建响应式网站，其中最为有名的两个是Bootrap和Foundation。

尽管这两个项目都十分棒，尤其是在学习如何搭建响应式视觉效果方面，但我仍然认为在生产中应该避免使用它们。

我和很多一开始使用了其中一个框架，最后却要修改它修改满足需求的开发者谈过。

这种方法在快速制作原型方面有巨大的优势，例如：把交互方式展现给客户看，但我认为把它加入到生产项目中是一种错误的策略。

首先，从技术上看，添加一个框架会为你的项目带来过多的冗余代码。
其次，从美学的角度上看，因为这种框架十分普及，所以你的项目会和无数个其他项目看起来一模一样。

最后，如果你只是在你的项目里复制粘贴代码，然后调整至符合你的需求，那么你不可能充分了解它们的原理。只有通过定位和解决你遇到的问题，你才能掌握你项目中的代码。

## 采用务实的解决方案

当涉及前端Web开发的时候，我总会为“象牙塔里的理想主义”而头疼。

在尝试去做“正确”的事情时，我们要尽可能选择务实的做法。

假设我们有一个按钮可以打开离屏菜单。
我们的自然反应可能会是这么编写：

```
<button class="menu-toggle js-active-off-canvas-menu">
    <span aria-label="site navigation">&#9776;</span> menu
</button>
```

美观又简单。
因为它是按钮，所以我们使用了button元素。

我们在按钮上使用了两个不同的HTML类，一个会是CSS样式的钩子（menu-toggle)，而另一个则是 JavaScript 钩子 (js-active-off-canvas-menu)。

另外，我们使用了arial-label属性来告诉屏幕读取器span元素中字符的意义。

在本例中，我们使用了 &#9976; 这是一个Unicode字符，代表了八卦中的天卦。

它被用在这里，仅仅是因为它和象征菜单的“汉堡图标”十分相像。

```
如果你想获取关于何时以及如何使用aria-label属性的建议，我强烈推荐Heydon Pickering 在 Opera 开发者网站上编写的这篇文章： 

https://dev.opera.com/articles/ux-accessibility-aria-label/
```

此时，我们的状态还是十分不错的。
语义化、简易的标记和功能区分完整的类。

下面，让我们调整一下样式吧：

```
.menu-toggle {
    appearance: none;
    display: inline-flex;
    padding: 0 10px;
    font-size: 17px;
    align-items: center;
    justify-content: center;
    border-radius: 8px;
    border: 1px solid #ebebeb;
    min-height: 44px;
    text-decoration: none;
    color: #777;
}

[aria-label="site navigation"] {
    margin-right: 1ch;
    font-size: 24px;
}
```

然而这并不是我们想要的。在这种情况下，浏览器觉得我们走得太远了。

Firefox不允许将一个按钮元素设置为Flex容器。这令开发者十分纠结。

我们应该选择正确的元素还是正确的外观效果呢？

理想状态下，我希望“汉堡图标”在左侧，而文字“menu”在右侧。

```
你可以在上例代码中看到我们使用了appearance属性。
它用于移除浏览器对于表单元素的默认样式，并且拥有一段简短的历史。
它是由W3C规定的，但是不久之后就被抛弃了，只剩下在Firefox和Webkit内核浏览器上带有浏览器前缀的版本。

万幸的是，现在它重新回到了规范中：

https://drafts.csswg.org/css-ui-4/#apperance-switching
```

**使用链接代替按钮**

我不得不承认，在这种两难的情况下，我通常会选择后者。
然后我努力弥补我使用错误元素的事实，方式是选择次优元素，修改它的ARIA角色来让其和正确的元素表现一致。

在本例中，我们的菜单按钮不是一个链接（毕竟，它不会跳转到任何地方），它只是一个为我所用的标签。

**我使用链接元素的原因是它比其他元素都更像按钮元素。**
而通过使用链接元素，我们可以实现梦寐以求的外观此效果。

下面是我编写的标记。

注意，我在a标签上添加了ARIA角色来表示它的功能是按钮（而不是默认的链接）：

```
<a class="menu-toggle js-activate-off-canvas-menu" role="button">
    <span aria-label="site navigation">&#9776;</span> menu
</a>
```

尽管这不完美，但确实是一个务实的解决方案。

当然，在这个简单的例子里，我们可以将display从flex改为block，然后使用padding来达到我们需要的外观效果。

又或者，我们可以继续使用button元素，然后将另外一个语义上无意义的元素（span）作为Flex容器来包裹它。

你可以根据自己的喜好来权衡使用哪种方法。

归根到底，是由我们自己来使文档标记更为合理。
有的开发者会有一个极端的想法，只使用div和span来确保浏览器上没有不想要的样式效果。
代价是他们的元素没有内在含义，换言之，可访问性较差。
而另一个极端则是标记纯粹主义者，他们认为使用正确的标记是最重要的，无论 视觉效果最终看起来如何。我认为，折中是更为明智和有效的做法。

## 尽可能使用最简单的代码

新技术提供的帮助的确很迷人。
但是要记住，使用最简单的方式去达到你的目的。
例如，如果你需要为列表中的第五个元素添加不同的样式，并且你能操作标记，那就不要像下面这样使用nth-child选择器：

```
.list-item: nth-child(5) {
    /* 样式 */
}
```

如果你可以操作标记，直接在标记上添加HTML类是更为明智的做法：

```
<li class="list-item specific-class">Item</item>
```

然后使用类来添加样式：

```
.specifi-class {
    /* 样式 */
}
```

它不仅更易懂，而且支持度也更高。

因为，旧版本的IE浏览器并不支持nth-child选择器。

## 根据视口隐藏、展示和加载内容

在响应式Web设计中有一个常用的准则：如果你在小屏幕上不加载某一部分，那么在大屏幕上也不应该加载。

这意味着在每一个视口下用户都应该能达到同样的目的，购买产品、阅读文章、完成交互。这是常识。毕竟作为用户，如果只是因为屏幕尺寸问题而不能在网站上进行操作，我们会感到失落。

这也同样意味着，随着屏幕的尺寸越来越大，我们也没有必要去增加额外的部分（窗口小部件、广告、链接等）来填充空白。如果没有了这些额外的部分，用户也能在小屏幕中良好地使用，那么在大屏幕里他们也应该问题不大。

在较大尺寸的视口里展示额外的部分也就意味着，要么在小视口里隐藏部分元素（通常是使用CSS中的display:none），要么在某种特定的视口下进行额外的加载（在JavaScript的帮助下）。

简洁而言，要么是部分内容被加载了但不可见，要么是部分内容可见但尚未加载。

广义地说，我认为上面的准则十分中肯。
如果贯彻下去，能够让设计师和开发者透彻地思考如何安排页面中的内容。
然而，就像以往的Web设计一样，总是会有例外的。

我总是尽量避免在不同的视口上加载新的标记，但是有时这是必需的。
我曾经编写过一个复杂的交互界面，需要在更宽的视口里加载不同的标记和设计。

在这种情况下，JavaScript用于将一个去区域中的标记替换掉。
这不是理想的情况，但这是最为务实的做法。
如果因为种种原因JavaScript失败了，用户可以得到较小的视口布局。
他们仍然能够进行想要的操作，这是我在当时条件下最好的实现方式。

随着你编写的响应式Web设计越来越多，你会遇到各种各样的选择，你需要自己判断在给定的情景下哪种选择更好。

不过，使用 display: none 来隐藏某些元素从而达到目标也不是一个坏方法。

**将复杂的可视化工作交给 CSS**

事实已经证明，JavaScript可以实现单独使用CSS无法实现的交互效果。
然而，如果可能的话，在涉及视觉效果的时候，我们仍然应该将工作交给CSS来完成。

这意味着，不要单独使用JavaScript实现菜单移入、移出、打开、关闭的动画效果。

说的就是你正在使用的jQuery的show和hide方法。

相反，使用JavaScript在相关的部分上做简单的类变换，然后让类去触发CSS展示相关的动画效果。

```
为了确保性能，在改变类的时候，请保证你改变的类尽可能与你的目的相关。
举个例子，如果你想让弹出框出现在某个元素上，那么在它们两共享的最近的父元素上添加相关类。

这将确保只有相关的部分变“脏”，而不用重绘广大的页面区域，从而保证性能。

如果想学习更多关于性能优化方面的知识，可以参考 Paul Lewis的 “浏览器渲染优化” 课程：

https://www.udacity.com/course/browser-rendering-optimization--ud860

```

## 验证器和代码检测工具

总的来说，HTML和CSS的容错性十分好。
你可以错误地嵌套、漏写引号或者忘记闭合标签，然而却一点问题没有。

尽管如此，几乎每周我都会被错误的标记所迷惑。

有的时候可能是一时手滑打错了字符，有的时候像一个小学生那样将div嵌套在span里，因为span是一个inline元素而div是一个block元素，这样会造成不可预测的结果。

万幸的是，有工具可以帮助我们。

在最坏的情况下，如果你遇到一个奇怪的问题，可以前往 https://validator.w3.org , 然后在上面粘贴你的代码。 它会指出所有的错误并且附上相应行数，帮助你修复。

更好的方法是为你的HTML、CSS和 JavaScript安装和配置检测工具。
又或者选择一款内置有代码检测工具的文本编辑器。

然后在你开发的时候，所有的问题都会被标记出来。

笨拙的我把width拼写成了width。
编辑器马上就发现了，并且之处了我的错误，还提供了一些修改建议。
尽可能地去使用这些工具吧。

这比花大量时间在代码里查找简单的语法错误更有意义。

## 性能

对于响应式Web设计，性能和外观一样重要。
然而，性能的衡量标准总是会变化。
例如，浏览器更新并改进它们处理资源的方法，发现了足以代替当前的“最佳方法”的新技术，技术终于被浏览器广泛支持，可以被广泛采纳了。

这样的例子不胜枚举。

不过仍然有一些基础条例是十分稳定的。好吧，到HTTP2普及后，它们中的许多都会被废弃掉。

1. 减少你的资源数（例如，不要加载15个JavaScript文件，而应该将它们拼成一个）。

2. 减少你的页面大小（如果你能压缩图片，那么请压缩）。

3. 延迟加载非必需资源。 如果你可以将CSS和JavaScript的加载延迟到页面加载完成后，就可以大幅缩短初始化事件。

4. 保证页面尽快可用。通常是上述所有步骤的副产物。

有很多工具可以度量和优化性能。
我最喜欢的是 https://www.webpagetest.org/。
它是最简单的，你只需输入一个网址然后点击START TEST即可。
它会显示出一份完整的页面分析。
不过更有用的是，它还会按照幻灯片的方式显示出页面的加载过程，让你知道如何改进页面加载速度。

当你尝试优化性能时，确保在开始前衡量性能表现，否则，你不知道你的优化工作的成果。

然后调整、测试、再重复上述步骤。

## 下一个划时代的产物

前端发展的一个有趣之处就是快速的改变。
总是有新事物要学习，而Web社区则孜孜不倦地挖掘更好、更快、更有效的解决问题的方式。

例如，在写本书的三年前，响应式图片就不存在。
想当年，我们只能使用第三方的解决方法来为不同的视口提供适合的图片。

同样，不久前，Flexbox只是在规范作者眼前一闪而过而已。
哪怕当其被写入规范，它仍然十分难用。直到Andrey Sitnik和他在Evil Martians上的聪明的合作人写出了Autoprefixer，我们才能相对轻松地跨浏览器使用它。

未来还会有更多令人兴趣的功能需要我们理解和实现。
我们已经在第4章提到了Service Workers。
它就是一个创建离线Web应用的更好的方法。

还有"Web组件"，它是一个规范集合，包括了影子DOM、自定义元素和HTML的引入方法。这些让我们得以创建完全定制的、可复用的组件。
]';lkjhnlkjgvxz,.,jgfz  ZSf'\
];jgtu9
ZXnb
-[0uytre]
然后还有其他接下来会被改进的地方，例如CSS4的选择器和CSS4的媒体查询。

最后，另一个隐约可见的重要改变就是HTTP2了。
它承诺将会让目前许多所谓的“最佳方法”变成“糟糕的方法”。

如果你想深入了解，我推荐你阅读Daniel Stenberg的 "http explained"。

如果你只是想阅读一个简短的总结，可以阅读Matt Wilcox的文章 ["前端开发者需要了解的HTTP2" ](https://mattwilcox.net/web-development/http2-for-front-end-web-developers)。