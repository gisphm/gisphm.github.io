---
layout: post
title: 将mercurial仓库转换成git仓库
---

### 起因
一般在`github`上找vim的仓库，都会被搜索引擎引导到这位的[`vim仓库`][1]。但是很可惜，这个仓库从8月31号后就没更新过，不知道仓库的作者是因为什么而没有同步[vim的mercurial仓库][2]。

### 解决
因为[vim的mercurial仓库][2]是用`mercurial`管理的，而`github`只提供了`git`支持。那么中间需要一个转换，不然只是单纯地`git init`，然后`git commit`，最后`git push`，是没有什么意义的，中间的许多变化、日志全没了。

谷歌一会后发现，`stackoverflow`或者是一些个人博客都基本是指向两个工具，一个是[`hg-git`][3]，另一个是[`hg-fast-export`][4]。当然也有提到[`git-remote-hg`][5]，不选择这个工具，是因为这个工具要重新把仓库克隆一遍，而我的想法是直接在本地已经克隆下来的仓库里改改就行了，所以没采用这个工具。

`hg-git`其实挺麻烦的，最主要的是我没安装成功，或者说这个插件没能工作。

`hg-fast-export`相当简单，把其[github仓库][4]克隆下来后，就可以使用了。我还参照了[这位博主的博文][6]进行操作，他是在mac上进行操作的。

我把`vim仓库`放在source文件夹下，然后新建一个仓库叫`vim-mirror`（`git init vim-mirror`）。进入这个空仓库后，执行`hg-fast-export.sh`的命令，进行递归转化。转化的结果是相当不错，不仅把日志转换了，还把tag转换了。当然工具并不是完美的，后面会有一些fatal的东西，是关于仓库的分支的一些信息，不过基本不用打理这个。最后就是一个`git checout HEAD`就算转换完成了。当mercurial仓库有更新时重复执行这个输出命令就行了，它会自动更新。

过程如下：
{% highlight bash %}
cd source
git clone https://github.com/frej/fast-export.git
git init vim-mirror
cd vim-mirror
~/source/fast-export/hg-fast-export.sh -r ~/source/vim
git checout HEAD
{% endhighlight %}


[1]: https://github.com/b4winckler/vim.git
[2]: https://code.google.com/p/vim
[3]: https://github.com/schacon/hg-git
[4]: https://github.com/frej/fast-export
[5]: https://github.com/felipec/git-remote-hg
[6]: http://hivelogic.com/articles/converting-from-mercurial-to-git/
