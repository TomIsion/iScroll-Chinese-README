# iScroll 给你的页面带来丝般顺滑的感受

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

目前我们提供这些种类的香水供你盛装出席：

- **iscroll.js**

## 快速开始

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

初始化的第二个参数对象可以配置 `iScroll` 的各项表现

在初始化后，可以通过返回值的 `options` 属性获取配置

### 动起来的核心

**以下三个属性通常都是不需要手动配置的，但是当你发现卡顿或是性能丢失时，你需要回来查看是不是哪个出现了问题**

// @todos：transform & translate

#### options.useTransform (Default: true)

关闭的话使用 `top/left` 来绘制动画，让人想起了被IE支配的恐惧，往往只用于 `Flash,iframes,video` 这些标签，同时这个属性意味着巨大的性能损耗

#### options.useTransition (Default: true)

关闭的话使用`requestAnimationFrame`来绘制页面，现代浏览器上区别不大，老旧浏览器上 `transition` 的效果更好

#### options.HWCompositing (Default: true)

增加 `translateZ(0)` 来优化移动端的效果

### 个性化你的 iScroll

#### options.dounce (Default: true)

开启缓动效果，如果你想追求完美相同，那就关了吧（那你还用毛`iScroll`）

#### options.click (Default: false)

为了近乎原生般的滚动体验，`iScroll` 默认禁止了很多的事件监听，如果你需要的话，手动开启这个事件。当然，我们管家推荐使用 `tap` 事件监听

#### options.disableMouse (Default: false)
#### options.disablePointer (Default: false)
#### options.disablePointer (Default: false)

// @todos：多个事件监听，但是只触发一个是如何做到的？

默认情况下，`iScroll` 会同时监听上面所有的事件，但是只会响应第一个被触发的事件。看上去这种行为有些资源浪费，但是为了最好的兼容性，放弃特征检测选择全部监听是最有效的方式了

如果你有强悍的内部检测机制，或者确定只需要其中的一种事件监听，那好吧，你可以关闭你所不需要的

```
var myScroll = new IScroll('#wrapper', {
  disableMouse: true,
  disablePointer: true
})
```

#### options.eventPassthrough (Default: false)

Todos

需要配合使用，具体作用不详

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

两者一起食用更佳

#### options.keyBindings (Default: false)

设置成 `true` ，使得键盘（遥控器）的操作变得有效，具体使用在后面详细介绍

#### options.invertWheelDirection (Default: false)

Todos

#### options.momentum (Default: true)

当用户快速点击页面的时候，动量的动画将会被触发。关闭这个效果会有效提升性能

#### options.mouseWheel (Default: false)

监听鼠标滚动事件

#### options.preventDefault (Default: true)

Todos 具体作用不详

#### options.scrollbars (Default: false)

是否显示默认的滚动条，具体使用在后面详细介绍

#### options.scrollX/.scrollY (Default: scrollX: false, scrollY: true)

正确的手动关闭对应方向的滚动监听，可以优化性能损耗

#### options.startX/.startY (Default: 0)

默认情况下 `iScroll` 从坐标 `0, 0` 开始，可以手动指定**初始化时开始的位置坐标**

#### options.tap (Default: false)

设置成 `true`，可以让 `iScroll` 对象监听 `tap` 事件，你可以像下面的方式来监听点击/轻触事件

```
document.getElement('#element').addEventListener('tap', doSth, false) // Native
$('#element').on('tap', doSth) // jQuery

// is iScroll
tap: true
```

### Scrollbars 相关

scrollbar的属性并不是像名字那么简单，事实上我更愿意把相关的设置归类为*指示器*的实现

看上去这个指示器只是显示根据滚动的位置然后变化其相对整体的位置，但是它真正能做的多得多

来，让我们慢慢来

#### options.scrollbars (Default: false)

// @todos：样式是如何实现的？ 默认实现的么

就和基础设置里面说的一样，把这个属性改成 `true` 是后续让指示器变得更有趣的先决条件

#### options.fadeScrollbars (Default: false)

没有使用滚动条或是静止时，`scrollbar` 会逐渐消失，`false` 会避免资源浪费

#### options.interactiveScrollbars (Default: false)

滚动条变得可拖拽，更富有交互性

#### options.resizeScrollbars (Default: true)

滚动条的长度会随着滚动容器和滚动区域的比例而变化。关闭自适应的尺寸效果可以设置固定长度的滚动条。常常配合用户自定义滚动条样式来使用

#### options.shrinkScrollbars (Default: false)

当滚动超出边界的时候，滚动条也会小小的收缩

可选的属性有 `'clip'` 与 `'scale'`

- `'clip'`：实现的原理只是把指示器移出了容器，看上去像是滚动条变小了然而事实上只是简单移动位置。如果可以接受这种呈现效果，这种选项会极大提升整体的性能
- `'scale'`：实现上会停止所有的 `useTransition`，而使用 `requestAnimationFrame` 来实现所有的动画。因而指示器大小在变化，因而在视觉上效果会更加优秀

值得注意的是，GPU不能进行重绘的操作，所以 `scale` 都是基于CPU进行计算

因为 `'clip'` 的效果依赖环境响应能力，所以最佳实践应该是跨平台产品使用 `'scale'`，移动端可以采用 `'clip'` 

#### 美化你的滚动条

不满意默认的滚动条样式，提供了下面的方式来

通过设置 `scrollbars` 选项是 `custom` 可以开启自定义滚动条样式，然后配合自定义对应类名的样式，就可以实现自定义的滚动条

- .iScrollHorizontalScrollbar 垂直方向上的滚动指示器的容器样式
- .iScrollVerticalScrollbar 同上，水平方向的容器样式
- .iScrollIndicator 滚动指示器的样式
- .iScrollBothScrollbars 当两个方向的滚动指示器同时出现的时候，这个样式会被自动添加到容器上面，主要目的是为了避免出现滚动条容器出现的重合的样式

最佳实践在手动指定 `iScroll` 样式的同时，不要去固定滚动条指示器的宽度，让他默认自适应大小

### 指示器

上面的滚动条相关设置都是面向指示器容器的设置，下面才是真正炫酷的指示器的设置，先举个栗子：

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

这是个指令式的参数，保存了对滚动条容器元素的引用。在容器中的第一个子元素将被认为是指示器。值得注意的是，滚动条可以出现在你文档的任何地方，而不是仅仅出现在滚动的容器里面。现在你开始意识到这个工具的威力了吧？

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

让指示器无视容器的边界。后续我们会了解到，我们可以修改指示器的移动速率，这样可以看上去只有指示器在移动（视差）。假设你让指示器的速度两倍于页面滚动的速度，很快指示器就会滚动到页面底部，所以这个属性常常用于配合实现视差滚动

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

// @ todos minmap的实现太酷炫 官方也没有讲清楚

不要混淆概念以及交叉使用，这样问题会很多

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