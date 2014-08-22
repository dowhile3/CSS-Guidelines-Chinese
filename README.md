CSS-Guidelines-Chinese
原文来自： http://cssguidelin.es/ 
版权所有： Harry Roberts

======================

CSS Guidelines 中文版

####简介

虽然易学好用，但 CSS 不是一门美妙的语言。无论在何种情况下很快它就会出差错。虽然我们无法改变 CSS 如何运作，但却可以改变自己的工作方式来适应它。

大型持久的项目通常有几十个不同的开发者，每个人能力和专长都不同，所以所有人用统一的方式协调工作便很重要

* 使样式表可维护。
* 使代码透明、正常和可读。
* 使样式表可扩展

有各种各方的方式可以满足这些目标，CSS Guideline 列出了一些建议和方法来帮助我们实现它们。

####风格指南的重要性

风格指南对于以下这种团队来说是一个宝贵的工具：

* 项目已经开工了一段时间
* 有技能多样化的开发者
* 一个组内有许多不同的开发者
* 经常有新人加入
* 有一些经常需要修改的代码

虽然风格指南更适用于对于大项目和持续长期运转的项目，在这些项目中，每一位开发者都应该尽力的标准化自己的代码。

当我们遵循一份好的风格指南的时候

* 为这个代码库设定标准
* 统一代码库的风格
* 给开发者一种熟悉感
* 提高生产力
 
风格指南必须透过各种方式透彻的被理解，并且应用到每一个项目中，无论何时何地。任何违反指南的都需要纠正。

####免责声明

CSS 指南是只是多种风格指南中的一个，其中和方法、技巧和小贴士，我会真诚的推荐给我的客户和团队。当然是你个人的洗好和面临的情况可能不同，请自取所需。

虽然这些指南参杂个人的看法，但是它们在多年里在大小项目中被反复的试错和精炼过。

================

####语法和格式
最简单的风格指南含有一系列的语法和格式。借助标准来写 CSS 意味着对团队所有成员来说，代码看上去和感觉上会很熟悉。

而且，看上去干净的代码感觉也干净，这意味着更好的工作环境，并且也让团队的成员们来一起维护好这个环境。丑陋的代码会带来不好的习惯。

在非常高的层级上，我们希望：At a very high-level, we want

* 4 空格缩进，不用 tab。
* 每行 80 字符宽
* 多行 CSS
* 合理使用空格

但是，这些都不是重要的，重要的是持之以恒。

####多文件

随着预处理器的流行，开发者越来越经常把 CSS 分割成多个文件。

即使不使用预处理器，把代码分割成独立的区块后再重组也是个好注意。

无论什么原因，假如你不用多个文件，下一章的内容需要做些许调整来满足你的习惯。

####目录

虽然打理目录需要花费较多的精力，但是它带来的好处大大超过复旦。细心的开发者不断更新文档，这是值得的。一份最新的目录能够告诉团队，这个 CSS 项目里有什么，做什么，次序如何。

一份简单的目录能够按顺序指出不同的栏目做什么，并给出一份总结，例如

```CSS
/**
 * CONTENTS
 *
 * SETTINGS
 * Global...............Globally-available variables and config.
 *
 * TOOLS
 * Mixins...............Useful mixins.
 *
 * GENERIC
 * Normalize.css........A level playing field.
 * Box-sizing...........Better default `box-sizing`.
 *
 * BASE
 * Headings.............H1–H6 styles.
 *
 * OBJECTS
 * Wrappers.............Wrapping and constraining elements.
 *
 * COMPONENTS
 * Page-head............The main page header.
 * Page-foot............The main page footer.
 * Buttons..............Button elements.
 *
 * TRUMPS
 * Text.................Text helpers.
 */
```
每一个项目对应一个章节

大的项目，目录的内容自然就大，但是仍然可以给开发者提供一个非常清晰的视觉：这是做啥的？以及为什么要用他。

####80字符宽

尽可能的限制 CSS 的行宽在 80 字符之内，原因是：

* 方便并列展示多个文件。
* 在 Github 等网站或终端中查看 CSS。
* 评论在这种宽度下看起来较合适

```CSS
/**
 * I am a long-form comment. I describe, in detail, the CSS that follows. I am
 * such a long comment that I easily break the 80 character limit, so I am
 * broken across several lines.
 */
```
像 URL，渐变语法等必须要保持在一行中，我们不必担心这种情况。

####标题

CSS 项目中的每一个主要栏目都需要附上标题：
```CSS
/*------------------------------------*\
    #SECTION-TITLE
\*------------------------------------*/

.selector {}
```
栏目的标题以#号起头，以便我们更好的搜索（例如用 grep 命令）：因为直接搜索标题会出来许多结果，而用了#号则只会返回你搜索的那个标题。

在标题和下一行代码间加入回车（无论那行代码是评论，Sass 或者 CSS）

如果这个项目中，每个栏目都有自己的文件，那么标题应该在每个文件的顶部。如果一个文件内有几个栏目，每个标题前应插入 5 个回车。额外空格和标题让寻找变得更加简单。

```CSS
/*------------------------------------*\
    #A-SECTION
\*------------------------------------*/

.selector {}





/*------------------------------------*\
    #ANOTHER-SECTION
\*------------------------------------*/

/**
 * Comment
 */

.another-selector {}
```

####规则的解析
开始动手前，先让我们熟悉相关名词的含义
```CSS
[selector] {
    [property]: [value];
    [<--declaration--->]
}
```

例如：
```
.foo, .foo--bar,
.baz {
    display: block;
    background-color: green;
    color: red;
}
```

从以上的例子我们可以看到：

* 相关的 selector 在同行，不相关的 selector 换行
* 大括号（{）前有一个空格
* 属性和值在同一行
* 分割属性和值的冒号（:）后有一个空格
* 每个声明占一行
* 开大括号和最后一个 selector 在同一行
* 第一个声明在开大括号的后一行
* 闭大括号自起一行。
* 每一个声明缩进 4 个空格
* 最后一个声明包含单冒号
这个格式几乎已经成为标准（除了空格数不同，有些开发者喜欢用两个空格）

因此，下面的是错误的
```
.foo, .foo--bar, .baz
{
	display:block;
	background-color:green;
	color:red }
```
错误的问题有：

* 使用 tab 而不是空格
* 不相同的 selector 在同一行上
* 开大括号自起一行
* 闭大括号没有自起一行
* 最后一个声明尾部的半冒号缺失。
* 冒号后无空格。

####多行CSS

除了非常特殊的情况，CSS 应该分多行写。这样做有许多好处：

* 因为每一段功能在自己行上，因此能减少合并冲突的机会。
* 更「真实」和可靠的 diffs，因为每行只有一个变动，

如果规则只有一行声明，那么就不必再起行，例子见下
```CSS
.icon {
    display: inline-block;
    width:  16px;
    height: 16px;
    background-image: url(/img/sprite.svg);
}

.icon--home     { background-position:   0     0  ; }
.icon--person   { background-position: -16px   0  ; }
.icon--files    { background-position:   0   -16px; }
.icon--settings { background-position: -16px -16px; }
```
单行的好处是：These types of ruleset benefit from being single-lined because

* 依然符合「每行一个变动」的规则
* 因为他们彼此相似，因此不需要像其他的规则那样细读，看 selector 比看声明更重要。

####缩进

和缩进独立的声明类似，缩进整个规则块能显示他们之间的关系，例如：
```CSS
.foo {}

    .foo__bar {}

        .foo__baz {}
```
这么做，开发者一眼就能看到， .foo__baz {} 在 .foo_bar {} 内， .foo__bar{} 在 .foo{} 内。

这种模拟 DOM 分层的办法，让开发者不要看到 HTML 也能够了解 class 的信息。

####缩进 SASS
SASS提供了嵌套的功能，例如：
```SASS
.foo {
    color: red;

    .bar {
        color: blue;
    }

}
```
编译了后会得到
```CSS
.foo { color: red; }
.foo .bar { color: blue; }
```
缩进 SASS 时，我们仍用 4 个空格。嵌套规则的前后各留一个空格。

N.B. 在 SASS 中要避免嵌套，Specificity 一章有更多的解释。

####对齐
对齐声明中常见和相关的字符串，例如：
```
.foo {
    -webkit-border-radius: 3px;
       -moz-border-radius: 3px;
            border-radius: 3px;
}

.bar {
    position: absolute;
    top:    0;
    right:  0;
    bottom: 0;
    left:   0;
    margin-right: -10px;
    margin-left:  -10px;
    padding-right: 10px;
    padding-left:  10px;
}

```
对使用支持栏编辑的开发者来说，这会更方便，他们可以一次性的修改多栏中的内容

####有意义的空格

和缩进类似，我们也可以在规则间加入任意或特定的空格。我们适应:

相关的规则间空一行
不很相关的规则间空二行
新的栏目间空五行
例如：
```CSS
/*------------------------------------*\
    #FOO
\*------------------------------------*/

.foo {}

    .foo__bar {}


.foo--baz {}





/*------------------------------------*\
    #BAR
\*------------------------------------*/

.bar {}

    .bar__baz {}

    .bar__foo {}
```
两个规则之间必须要有空行，以下的是错误的：
```CSS
.foo {}
    .foo__bar {}
.foo--baz {}
```

####HTML
因为 HTML 和 CSS 本质上互相搅和在一起，因此不谈 HTML 的语法和格式规范便显得有些奇怪。

永远给参数加上引号，即便不加也可以。这样会减少出错的机会，并且对大多数开发者来说是更熟悉的格式。以下的是可用的：
```CSS
<div class=box>
```
但是这个格式更好
```
<div class="box">
```
以上的引号不是必须的，但为了安全还是加上它。

当在一个 class 的参数中包含多个值的时候，用两个空格分隔他们：
```CSS
<div class="foo  bar">
```
当多 class 互相关联，用中括号来分组，例如：
```CSS
<div class="[ box  box--highlight ]  [ bio  bio--long ]">
```
我不强烈推荐这么做，也怀疑这种做法，但是这么做仍然是有一些好处的。想了解更多的话，请读[在文档中组合相关的 class](http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/) 。

和 CSS 规则相似，也可以在 HTML 中通过加空格来标记含义，例如，在区段间加入五行空行：

```HTML
<header class="page-head">
    ...
</header>





<main class="page-content">
    ...
</main>





<footer class="page-foot">
    ...
</footer>
```
用单行的空行来分割独立但不相关的区段，例如：
```HTML
<ul class="primary-nav">

    <li class="primary-nav__item">
        <a href="/" class="primary-nav__link">Home</a>
    </li>

    <li class="primary-nav__item  primary-nav__trigger">
        <a href="/about" class="primary-nav__link">About</a>

        <ul class="primary-nav__sub-nav">
            <li><a href="/about/products">Products</a></li>
            <li><a href="/about/company">Company</a></li>
        </ul>

    </li>

    <li class="primary-nav__item">
        <a href="/contact" class="primary-nav__link">Contact</a>
    </li>

</ul>
```
开发者一眼就能看到 DOM 的成分，也使得某些文本编辑器，例如 Vim 来操控用空行隔开的标记。

####评论

CSS 带来的精神上的负担是巨大的。有许多东西需要知道，有很多和项目有关的细节要去记，开发者遇到最糟糕的情况是面对其他人写的代码。记住自己的 class、规则、对象和助手不难，难得是理解其他人的。

CSS 需要更多的评论。

因为 CSS 是声明性的语言，所以很难透过字面意思，单单看 CSS 去了解它的含义

* 有些 CSS 可能仰赖其他的代码
* 某段代码对其他效果的影响
* 代码的复用
* 继承了怎样的样式（刻意或者无意）
* 传递了怎样的样式（刻意或者无意）
* 作者想把样式放在哪里

这里甚至没有考量 CSS 的诸多奇异特性，例如多种 overflow 触发的块格式、或者某些 transform 属性触发硬件加速，这对接手的开发者来说更加的麻烦。

因为 CSS 无法很好的描述自己的情况，这是一个非常需要注释的语言。

一个规则是，注释任何一眼不能看穿的代码。意思就是，不需要告诉大家颜色的含义，但是如果使用 overflow: hidden 来去除浮动，而不是用来截去某个元素的 overflow，那么这就值得记录。


####高层

对于记录整个分段或组件的大块评论来说，使用 DocBlock 级的多行评论，每行 80 字符宽。

这是来自 CSS Wizardry 网站中记录页头的真实例子：
```CSS
/**
 * The site’s main page-head can have two different states:
 *
 * 1) Regular page-head with no backgrounds or extra treatments; it just
 *    contains the logo and nav.
 * 2) A masthead that has a fluid-height (becoming fixed after a certain point)
 *    which has a large background image, and some supporting text.
 *
 * The regular page-head is incredibly simple, but the masthead version has some
 * slightly intermingled dependency with the wrapper that lives inside it.
 */
```

这种级别的细节应该应用到任何状态、改变、情况、处理时的代码描述。

####对象扩展指针

When working across multiple partials, or in an OOCSS manner, you will often find that rulesets that can work in conjunction with each other are not always in the same file or location. For example, you may have a generic button object—which provides purely structural styles—which is to be extended in a component-level partial which will add cosmetics. We document this relationship across files with simple object–extension pointers. In the object file:
