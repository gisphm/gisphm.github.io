---
layout: post
title: 絮叨说配置vim
---

## 他山之石
之前没有想过要自己去独立配置vim，感觉里面的内容太多，过于复杂了。
如果要抄别人的来用，也是相当恐怖的工作量。
因为我所看到的好配置都是随便代码量超千的，长长的配置，要记的东西实在是太多了。
所以我都是拿别人配置得差不多的来用，比如[vimified][1]、[amix][2]、[janus][3]和[spf13-vim][4]。
以上四种都是可配置性高，包含各种必需的插件，针对各种语言的开发也有一些配置得差不多的插件了，
如果要自己加插件也是可以的。

经过一段时间的选择后，我选择了`spf13-vim`作为一个使用的基本配置，
在上面进行各种插件的加工。这个配置对自己的影响较大，现在的好多键盘映射习惯都是继承自它。
同时，它也帮助我更好地理解了`vim`和使用`vim`，虽然实际上自己对`vim`的很多部分依旧是一知半解。

## 自立更生
`spf13-vim`最近有更新，用[auto-pairs][5]取代了[vim-autoclose][6]，
但同时`ESC`和方向键的使用出现问题。方向键我倒不经常用，这个的问题不影响日常使用。
可进入`insert`模式后，`ESC`键需要多按几次才能退回到`normal`模式，这就烦人了。
原因应该是这个替换跟`omnicomplete`部分的“有用”映射出现冲突了，具体是怎么冲突的，
我也不太懂。我不清楚`auto-pairs`的源码里到底写了什么，导致这些个冲突发生了。

另一方面，在使用过程中，我也发现`spf13-vim`有许多不如自己意的地方。
可配置性虽然是比较高，但有时，某些定下来的东西是自己不希望的。
比如`wrap`，我是希望`vim`在使用时能自动换行，
但`spf13-vim`里默认是`nowrap`，而且固定是在了`.vimrc`里，无法覆盖。

于是，自己下定决心，搞一个合适自己的出来。

## 步步为营
从零开始是艰难的，因为不想直接一切都搬用`spf13-vim`。
自己之前弄过一个[neovim][7]的[配置][8]，当时的想法受到`spf13-vim`的启发，
把插件列表放一个文件里，插件的配置放另一个文件里，也还算用得不错，
只是`neovim`项目本身还不是很成熟，很多的语言绑定还没有开发完成。
导致现在的许多插件是不能用在`neovim`上的。

基本照着那个配置和复制大量的`spf13-vim`里的内容进行搞一通后，
发布了`v0.1`版本，结果自己无法使用。
`Vundle`初始化失败（原因至今不明）。几番尝试，还是不行。
于是在一气之下，用上了`neobundle`，结果一试就成功。赶紧整理一些插件配置，
发布了`v0.2`版本，用着倒是挺舒服。

于是后面的版本就在这种半尝试半配置的条件下陆续发布。一个比一个要好一点。
当然基本的框架想法是来自`spf13-vim`，可到后面，就完全按照自己的思路去搞了。
这个作者这里抄一点，那个作者那里抄一点，然后作一些评估。

## 有女初成
经过一两天时间的努力，基本就有了一个可用，且针对性较强的[配置][9]。
不敢说是最好的配置，但其可用性已经超过我的想像。
应对rails的一般编辑工作基本是没有压力了。
同时，这份配置里带了许多的web开发插件（可能会多了一点，以后考虑删除一些），对
html、javascript、css等文件的编辑也是相当有用的。

在这个配置过程里，我有以下几个总结：

1. 大牛们的可靠配置是最直接的（虽然不一定是最好的）、开箱即用的，也是最好的参照。

2. 自己在配置插件的过程中应该多参考插件的作者自己的一些默认配置，可以发现不少细节。

    > 比如，我在配置`neosnippet`的时候，更多地参考了作者`Shougo`自己的vimrc
    > 里的一些配置。

3. 仔细阅读插件的一些写法，可以更细致地让插件的使用更方便。当然，这也比较烦琐，特别是
一些插件的说明超长，拥有几百行甚至上千行的doc，需要耐心慢慢阅读，以理解作者的一些意图。
4. 插件一般都在github上有托管，关注一些重要插件的`issue`是相当有用的，能较及时发现一些
问题和可能错误的配置方式。
5. 最为主要的是，自己一定要有动力去改造或者创造一份配置，折腾无极限。

[1]: https://github.com/zaiste/vimified
[2]: https://github.com/amix/vimrc
[3]: https://github.com/carlhuda/janus
[4]: https://github.com/spf13/spf13-vim
[5]: https://github.com/jiangmiao/auto-pairs
[6]: https://github.com/spf13/vim-autoclose
[7]: https://github.com/neovim/neovim
[8]: https://github.com/gisphm/myneovimrc
[9]: https://github.com/gisphm/myvimrc