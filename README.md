# iScroll 给你的页面带来丝般顺滑的感受

- 原文链接： [https://github.com/cubiq/iscroll/blob/master/README.md](https://github.com/cubiq/iscroll/blob/master/README.md)
- 库链接： [https://github.com/cubiq/iscroll](https://github.com/cubiq/iscroll)

## 背景

`iScroll` 是表现优异、内存占用小、无依赖且支持多平台的使用 `javascript` 实现的滚动

它可以使用在桌面浏览器、移动端设置智能电视上。无论是现代还是远古的设备，`iScroll`  都提供了大幅的性能优化和大小压缩以能获得最顺畅的结果

`iScroll` 不是简简单单的 *scroll* 滚动事件。它不仅仅可以用来操作所有用户需要移动的节点元素，同时提供了滚动、缩放、平滑、无限滚动、视差滚动与轮播，实现这些玩意仅仅只需要 4kb 的大小。对了，给 `iScroll` 扫帚，它甚至可以帮你打扫办公室

甚至在很多平台上原生提供的滚动已经足够优秀，但是除此之外 `iScroll` 还会提供下面的特性

- 细微的动量感知，你随时可以获取、设置滚动区域的坐标位置
- 自定义的动画效果，通过自定义函数，可以实现诸如 `bounce`，`elastic`，`back` 等等的效果
- 各种各样的生命周期（钩子）函数，诸如 `onBeforeScrollStart`，`onScrollStart`，`onScroll`，`onScrollEnd`，`flick` 等等
- 强悍的兼容和降级能力，无论是老旧的安卓机还是最新的 iPhone，无论是 Chrome 还是 Internet，都能优秀兼容

## 多样化的 iScroll

`iScroll` 设计出来的初衷就是为了优化原有的滚动体现。为了这个目的，`iScroll` 被分割成了许多的版本，你可以根据需求来选择最合适你的版本来获得最佳体验。

目前我们提供这些种类的香水来供你盛装出席：

- **iscroll.js**
- ****

## 快速开始

废话不多说了，你肯定是想成为优秀的 `iScroll` 使用者。酷，跟上我，下面就来了

学习 `iScroll` 最好的方式就是通过许许多多的例子来学习。你可以在远程库的路径下发现一个 `demo` 路径里面塞满了各种例子，大多数的特性都可以在这些例子里面找到

`iScroll` 提供一个名叫 `IScroll` 的类，你要做的只是给每个需要滚动的区域初始化这个类。再遇到渲染、CPU/内存瓶颈之前，对于每个页面中可以有的 `iScroll` 对象的数量没有限制。

使你的DOM结构尽可能保持简单，`iScroll` 虽然可以自己创建DOM结构，但是对于DOM结构还是有个最基本的限制条件

最佳实践的HTML结构是：

```
<div id="wrapper">
    <ul>
        <li>...</li>
        <li>...</li>
        ...
    </ul>
</div>
```

`iScroll` 必须被滚动区域的容器所初始化。在上面的例子中就是想让 `UL` 节点滚动起来。**`iScroll` 必须作用于滚动区域的外层包裹DOM上，同时外层包裹的容器只有它的首个子节点才会有 `iScroll` 的滚动效果，其他子节点会被忽视**

<!-- @todos：这段翻译需要重置 -->

只需要 `IScroll(element)` 你所需要滚动的DOM结构就可以，但是请注意

### 表现

1. 纵向的滚动
2. 缓动的效果

### 作用对象

可以传递DOM结构，也可以传递原生支持的选择器

**`iScroll` 必须作用于滚动区域的外层包裹DOM上，同时外层包裹的容器只有它的首个子节点才会有 `iScroll` 的动画效果**

**多个容器需要初始化则需要手动循环，内部的实现是 `querySelector()`**

### 监听时刻
 
推荐在DOM元素加载完成之后初始化 `iScroll`。推荐监听 `window.onload()` 事件，其中注意图片加载最好通过样式限制高度，因为 iScroll 需要知道滚动区域的准确宽高，有的时候，一点点延时 100~200ms 也会解决很多的疑难杂症 

同时给滚动容器设置 `position: absoulte/relative` 会解决很多的计算错误的问题

// @todos：onload vs DOMContentLoaded 之间的区别

## 配置

通过指定初始化 `iScroll` 的第二个参数对象，可以配置 `iScroll` 的各项表现

在初始化后，可以通过返回值的 `options` 属性获取配置

### 动起来的核心

`iScroll` 基于设备/浏览器的能力检测，使用了许多不同的技术来实现滚动的效果。**通常情况下，不需要你来代替引擎选择何种技术**，`iScroll` 足够聪明，它足以帮你选择最优解

最重要的是明确当前 `iScroll` 运行在何种机制下

#### options.useTransform (Default: true)

默认情况下 `iScroll` 引擎会使用 `transform` 这个样式属性来变化位置。关闭的话使用 `top/left` 来绘制动画，让人想起了被IE支配的恐惧

关闭的情况往往只适用于 `Flash,iframes,video` 这些标签，同时关闭这个属性意味着巨大的性能损耗

#### options.useTransition (Default: true)

`iScroll` 使用样式属性 `transition` 来实现动画（尤其是动量变化与缓动效果）。关闭的话使用`requestAnimationFrame`来代替

现代浏览器上区别不大，老旧浏览器上 `transition` 的效果更好

#### options.HWCompositing (Default: true)

这个属性给滚动区域的样式属性中增加了 `translateZ(0)`。这大大提升了在优化移动端的呈现效果，但是如果你有过多的滚动区域同时硬件不能很好的支撑效果，你需要关闭这个配置项

如果不能确定是否需要改变这三个属性值，那就让 `iScroll` 来做最优配置的决定。为了获得最佳体验效果，上面这些可选的配置属性都应该被配置成为 `true` （或者干脆不配置它们，`iScroll` 会自动将他们配置成 `true`）。当你的程序出现卡顿或者是内存泄漏的情况，你需要考虑是不是需要关闭其中的某个或者某几个属性

### 个性化你的 iScroll

#### options.dounce (Default: true)

当滚动区域遇到边界的时候，将会有个小的反弹动画（和 `iOS` 下橡皮筋效果类似）。如果你想追求和老旧缓慢机型上效果完美相同，那就关了吧（那你还用毛`iScroll`）

#### options.click (Default: false)

为了近乎原生般的滚动体验，`iScroll` 默认禁止了很多的事件监听，譬如鼠标点击事件。如果你需要监听 `click` 事件，那么需要手动开启这个事件。当然，我们官方更加推荐使用 `tap` 事件监听而不是 `click`

#### options.disableMouse (Default: false)
#### options.disablePointer (Default: false)
#### options.disablePointer (Default: false)

默认情况下，`iScroll` 会同时监听上面所有的事件，但是只会响应第一个被触发的事件。看上去这种行为有些资源浪费，但是为了最好的兼容性，放弃特征检测选择全部监听是最有效的方式了

如果你有强悍的内部检测机制，或者确定只需要其中的一种事件监听，那好吧，你可以关闭你所不需要的

举个栗子，关闭鼠标与指针事件监听你需要这么做：

```
var myScroll = new IScroll('#wrapper', {
  disableMouse: true,
  disablePointer: true
})
```

#### options.eventPassthrough (Default: false)

有的时候，你需要保留原生的竖直滚动与此同时需要增加水平的 `iScroll` （可能是个轮播效果）。开启这个属性，那样 `iScroll` 仅仅只会监听水平方向的事件。竖直方向的滚动仍旧会与原来的保持一致

看这个移动端的例子 [event passthrough demo]()。需要注意的是，这个属性被设置后可能的展现效果是竖直方向的（原生的滚动方向是水平的，那么 `iScroll` 的方向就是竖直的）

#### options.freeScroll (Default: false)

当你既需要横向，也需要纵向滑动的时候，这个属性就变得很有效，没有这个属性的情况下，你只是加上

```
scrollX: true
```

`iScroll` 会当你开始一个方向的滚动时，另外一个方向就被锁死了，所以当你需要自由滚动的时候，配合

```
scrollX: true,
freeScroll: true
```

两者一起食用更佳，看这个栗子 [2D Scroll demo]()

#### options.keyBindings (Default: false)

设置成 `true` ，使得键盘（遥控器）的操作变得有效，看这个栗子 [Key bindings]()。具体使用在后面详细介绍

#### options.invertWheelDirection (Default: false)

当鼠标滚轮事件监听被开启时才会有作用，在这样的前提条件下，通过这个属性可以增加滚动方向（栗子：向下滚轮滚动的时候可以让页面向上滚动，反之亦然）。

#### options.momentum (Default: true)

当用户快速点击页面的时候，动量的动画将会被触发。关闭这个效果会有效提升性能

#### options.mouseWheel (Default: false)

是否开启监听鼠标滚轮相关事件

#### options.preventDefault (Default: true)

设置当事件被触发的时候，是否会执行 `preventDefault()` 事件。这个属性应该默保持 `true`，除非你真正明确想要的效果

在下面的高级特性中的 `preventDefaultException` 将会详细讲述相关组织默认事件效果的相关

#### options.scrollbars (Default: false)

是否显示默认的滚动条，具体使用在后面滚动条模块详细介绍

#### options.scrollX/.scrollY (Default: scrollX: false, scrollY: true)

默认情况下只会开启竖直方向上的滚动效果。如果你需要水平方向的滚动，你需要设置 `scrollX` 值为 `true`。看这个栗子 [horizontal demo]()

正确的手动关闭对应方向的滚动监听，可以优化性能损耗

#### options.startX/.startY (Default: 0)

默认情况下 `iScroll` 从坐标 `0, 0` 开始，可以手动指定**初始化时**开始的位置坐标

#### options.tap (Default: false)

设置成 `true`，可以让 `iScroll` 中滚动区域，你可以像下面的方式来监听点击/轻触事件

```
document.getElement('#element').addEventListener('tap', doSth, false) // Native
$('#element').on('tap', doSth) // jQuery

// in iScroll
tap: true
```



### Scrollbars 相关

scrollbar的属性并不是像名字那么简单，事实上我更愿意把相关的设置归类为*指示器*的实现

看上去这个指示器只是显示根据滚动的位置然后变化其相对整体的位置，但是它真正能做的多得多

来，让我们慢慢来

#### options.scrollbars (Default: false)

// @todos：样式是如何实现的？ 默认实现的么

就和`个性化你的 iScroll`里面各项属性设置一样，把这个属性改成 `true` 是后续让指示器变得更有趣的先决条件

```
var myScroll = new IScroll('#wrapper', {
  scrollbars: true
})
```

#### options.fadeScrollbars (Default: false)

没有使用滚动条或是静止时，`scrollbar` 会逐渐消失，`false` 会避免资源浪费

#### options.interactiveScrollbars (Default: false)

滚动条变得可拖拽，更富有交互性

#### options.resizeScrollbars (Default: true)

滚动条的长度会随着滚动容器和滚动区域的大小比例而变化。关闭自适应的尺寸效果可以设置固定长度的滚动条。常常配合用户自定义滚动条样式来使用

#### options.shrinkScrollbars (Default: false)

<!-- @todos：这段翻译需要重置 -->

当滚动超出边界的时候，滚动条也会小小的收缩

可选的属性有 `'clip'` 与 `'scale'`

- `'clip'`：实现的原理只是把指示器移出了容器，看上去像是滚动条变小了然而事实上只是简单移动位置。如果可以接受这种呈现效果，这种选项会极大提升整体的性能
- `'scale'`：实现上会停止所有的 `useTransition`，而使用 `requestAnimationFrame` 来实现所有的动画。因而指示器大小在变化，因而在视觉上效果会更加优秀

值得注意的是，GPU不能进行重绘的操作，所以 `scale` 都是基于CPU进行计算

因为 `'clip'` 的效果依赖环境响应能力，所以最佳实践应该是跨平台产品使用 `'scale'`，移动端可以采用 `'clip'` 

#### 美化你的滚动条

不满意默认的滚动条样式 / 你能做得更好？，提供了下面的方式来自定义你的滚动条

通过设置 `scrollbars` 选项是 `custom` 可以开启自定义滚动条样式，然后配合自定义对应类名的样式，就可以实现自定义的滚动条

- .iScrollHorizontalScrollbar 垂直方向上的滚动指示器的容器样式
- .iScrollVerticalScrollbar 同上，水平方向的容器样式
- .iScrollIndicator 滚动指示器的样式
- .iScrollBothScrollbars 当两个方向的滚动指示器同时出现的时候，这个样式会被自动添加到容器上面，主要目的是为了避免出现滚动条容器出现的重合的样式

这个栗子 [styled scrollbars demo]() 比我苍白的解释要有用得多

最佳实践在手动指定 `iScroll` 样式的同时，需要固定滚动条指示器的长度，自动计算往往会导致长度过小的情况

### 指示器

上面的设置都是相对简单原始的滚动条的设置，下面才是真正炫酷的指示器设置，先举个栗子：

```
var myScroll = new IScroll('#wrapper', {
    indicators: {
        el: [element|element selector]
        fade: false,
        ignoreBoundaries: false,
        interactive: false,
        listenX: true,
        listenY: true,
        resize: true,
        shrink: false,
        speedRatioX: 0,
        speedRatioY: 0,
    }
});
```

#### options.indicators.el

这是个指令式的参数，保存了对指示器容器元素的引用。在容器中的第一个子元素将被认为是指示器。值得注意的是，指示器容器可以出现在你文档的任何地方，而不是仅仅出现在滚动的容器里面。现在你开始意识到这个工具的威力了吧？

有效的语法：

```
  indicators: {
    el: document.getElementById('indicator')
  }
```

也可以写的简单些：

```
  indicators: {
    el: '#indicator'
  }
```

#### options.indicators.ignoreBoundaries (Default: false)

让指示器无视容器的边界。后续我们会了解到，借助这个属性同时修改指示器的移动速率，这样可以看上去只有指示器在移动（视差）。假设你让指示器的速度两倍于页面滚动的速度，很快指示器就会滚动到页面底部，所以这个属性常常用于配合实现视差滚动，看栗子 [parallax scrolling]()

#### options.indicators.listenX (Default: true)
#### options.indicators.listenY (Default: true)

指示器监听的变化轴，可以被设置成单方向或者两个方向

#### options.indicators.speedRatioX (Default: 0)
#### options.indicators.speedRatioY (Default: 0)

指示器相对滚动主体移动速率的比例关系。默认情况下这个属性会自动设置，你很少需要修改这个属性

#### options.indicators.fade
#### options.indicators.interactive
#### options.indicators.resize
#### options.indicators.shrink

这些属性的名称看上去我们在滚动条模块已经都介绍过了。在这里重复并不是我脑子坏了或是什么，你往下看就知道了

**不要混淆概念以及交叉使用，这样问题会很多！**

### 视差滚动

视差滚动效果只是多个指示器并行滚动的体现效果

指示器只是会跟随滚动主体元素滚动的一层元素。如果你能这样理解指示器，你就可以明白在酷炫的视差滚动背后的实现原理。你可以添加多个指示器然后就会看到更加明显的视差滚动

### 编程来控制滚动

使用编程来控制滚动才是最酷的

#### scrollTo(x, y, time, easing)

假设把 `iScroll` 的实例保存到了变量 `myScroll` 中，你可以通过下面的方法来使得它滚动到任何位置

```
myScroll.scrollTo(0, -100)
```

这样会使得 `iScroll` 对象向下滑动 100px。记住咯，0 代表了左上角的位置，`scrollTo` 相对左上角进行滚动，是绝对滚动，所以为了实现滚动，你需要传负数的数值

`time` 与 `easing` 是可选的参数，这俩分别控制滚动的时长（单位：ms）以及缓动函数效果。

你可以通过 `IScroll.utils.ease` 对象来获取缓动函数。举个栗子，1秒时长的橡皮筋缓动效果：

```
myScroll.scrollTo(0, -100, 1000, IScroll.utils.ease.elastic)
```

所有可选的缓动属性有这些：

- `quadratic` 
- `circular`  
- `back` 
- `bounce` 
- `elastic`

#### scrollBy(x, y, time, easing)

和上面的函数一样，不过变化的距离是相对元素变化前的位置，相对滚动

```
myScroll.scrollBy(0, -10)
```

将会向下滚动 10px，如果原本位置是 -100，那么现在位置就是 -110

#### scrollToElement(el, time, offsetX, offsetY, easing)

别着急，你会爱上这个函数的

唯一强制的参数是 `el`，传递一个DOM元素节点或是选择器，那么 iScroll 将会滚动到这个元素的左上角

`time` 可选参数，仍旧是控制滚动的时长（单位：ms）

`offsetX` 与 `offsetY` 以px为单位定义了偏移量，借助这两个参数你可以滚动到特定的元素外加指定的偏移量。不仅如此，通过设置这个属性为 `true`，那么容器将会滚动到使得指定元素位于屏幕中央的位置

`easing` 缓动函数和 `scrollTo` 方法中作用的方式一样

### Snap

`iScroll` 可以帮助你对齐位置和元素

#### options.snap

下面就是最简单的 `snap` 设置

```
var myScroll = new IScroll('#wrapper', {
  snap: true
})
```

这样，将会自动将滚动的区域分割成多页的效果，每页的尺寸是容器的大小

`snap` 同样也可以指定为字符串。字符串会被看做选择器，决定滚动区域将被分割成的单位元素，就像下面这样

```
var myScroll = new IScroll('#wrapper', {
  snap: 'li'
})
```

通过这样的设置，滚动区域中每个 `LI` 标签都会被分割出来

只是简单分割多页看上去什么都不能做，因而 `iScroll` 提供了一系列的方法来使分割变得更有趣

#### goToPage(x, y, time, easing)

`x` 与 `y` 分别代表了在水平、垂直方向上你想要滚动的页数。如果滚动区域只是在单方向上实现滚动，只需要传递 `0` 给那个不需要滚动的方向

`time` 是滚动的时长，`easing` 是用于指定缓动函数，参考后面**其他属性**中的[]()，他们都是可选的属性

```
myScroll.goToPage(10, 0, 1000)
```

这样将会在 1 秒的时间内水平移动到第 10 页的位置

#### next()
#### prev()

前往相对于当前位置的下一页或者上一页

### Zoom

为了体验更好的缩放、挤压功能，推荐使用 `iscroll-zoom.js` 版本

#### options.zoom (Default: false)

设置为 `true` 来开启缩放效果

#### options.zoomMax (Default: 4)

缩放的最大比例

#### options.zoomMin (Default: 1)

缩放的最小比例

#### options.startZoom (Default: 1)

开始时的缩放比例

#### options.wheelAction (Default: undefined)

如果把滚动事件改成 `'zoom'`，将会让滚轮事件修改缩放比例而不是触发滚动事件

总的来说，一个完备漂亮的缩放设置是下面这样的：

```
myScroll = new IScroll('#wrapper', {
  zoom: true,
  mouseWheel: true,
  wheelAction: 'zoom'
})
```

缩放的实现是依赖 `CSS transform`。`iScroll` 只能在浏览器支持 `CSS transform` 的情况下实现缩放

当待缩放的区域被渲染到页面上时，或者说当你开始对待缩放区域进行变换的时候，很多浏览器（尤其是 `webkit` 内核的浏览器）会保存一份缩放区域的快照。这份快照会作为缩放变化的基准，同时它几乎不可能更新。这就意味着，你的基准是一倍大小的元素，因此缩放会导致文字图片变得模糊不清

有个很简单的解决方案就是把缩放的大小设置为两倍（或者是三倍）于它本身的分辨率，然后把它包裹在 `scale(0.5)` 的div中。这样就足够给你个更好的结果。希望以后我能带来更多的演示

#### zoom(scale, x, y, time)

可以让你的缩放生动起来的方法

`scale` 是缩放的比例

`x` 和 `y` 是坐标值，缩放的中心点。如果没有指定的话，将会使用屏幕的中心点

`time` 还是老样子，毫秒单位的缩放变化时长（可选的）

### 无限滚动

`iScroll` 集成了优化的缓存系统，因而实现了通过使用（、复用）有限的元素来呈现无限的数据

无限滚动还处在早起的发展阶段，尽管看上去它是稳定可用的，但是还没有做好广泛的推广

在这里还是麻烦你帮我检阅无限滚动的代码，同时可以留下你的建议和错误报告

一旦功能有所变化或者有了进化，我会立刻更新这块内容

### 高级选项

为那些专家程序员所准备

#### options.bindToWrapper (Default: false)

// @todos：可以看到事件监听的不同，但是看上去没有区别

`move` 事件通常被绑定到 `document` 元素上而不是滚动的容器元素。


















## Tips

### 1. 慎用下面的样式

对硬件加速不友好，复杂的页面结构会出现延时和抖动

1. box-shadow
2. opacity
3. text-shadow

可以的话，使用背景图片来实现阴影