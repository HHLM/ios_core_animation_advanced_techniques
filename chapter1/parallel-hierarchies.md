# 平行的层级关系
&nbsp;&nbsp;&nbsp;&nbsp;每一个`UIview`都有一个`CALayer`实例的图层属性，也就是所谓的*backing layer*，视图的职责就是创建并管理这个图层，以确保当子视图在层级关系中添加或者被移除的时候，他们关联的图层也同样对应在层级关系树当中有相同的操作（见图1.2）。
<img src="./1.2.jpeg" alt="图1.2" title="图1.2" width="700"/>
图1.2 图层的树状结构（左边）以及对应的视图层级（右边）

&nbsp;&nbsp;&nbsp;&nbsp;实际上这些背后关联的图层才是真正用来在屏幕上显示和做动画，`UIView`仅仅是对它的一个封装，提供了一些iOS类似于处理触摸的具体功能，以及Core Animation底层方法的高级接口。

&nbsp;&nbsp;&nbsp;&nbsp;但是为什么iOS要基于`UIView`和`CALayer`提供两个平行的层级关系呢？为什么不用一个简单的层级来处理所有事情呢？原因在于要做职责分离，这样也能避免很多重复代码。在iOS和Mac OS两个平台上，事件和用户交互有很多地方的不同，基于多点触控的用户界面和基于鼠标键盘有着本质的区别，这就是为什么iOS有UIKit和`UIView`，但是Mac OS有AppKit和`NSView`的原因。他们功能上很相似，但是在实现上有着显著的区别。

&nbsp;&nbsp;&nbsp;&nbsp;绘图，布局和动画，相比之下就是类似Mac笔记本和桌面系列一样应用于iPhone和iPad触屏的概念。把这种功能的逻辑分开并应用到独立的Core Animation框架，苹果就能够在iOS和Mac OS之间共享代码，使得对苹果自己的OS开发团队和第三方开发者去开发两个平台的应用更加便捷。

&nbsp;&nbsp;&nbsp;&nbsp;实际上，这里并不是两个层级关系，而是四个，每一个都扮演不同的角色，除了视图层级和图层树之外，还存在*呈现树*和*渲染树*，将在第七章“隐式动画”和第十二章“性能调优”分别讨论。


