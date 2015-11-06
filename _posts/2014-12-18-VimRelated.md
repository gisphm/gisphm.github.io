---
layout: post
title: 与 Vim 相关
---

---

最开始接触 linux 时，只知道 `ls`这一条命令，其他的什么都不知道。

现在 linux 已经成为自己日常的一部分，一天不开就浑身难受。虽然并不是完全地理解了 linux，也不能自由地写 bash 或者 zsh 的 shell 脚本，但至少能简单地使用 vim 进行编辑，写程序。

也是从 Linux 开始，我学会了如何去翻“墙”。最开始只会用人家编译好的 vim，直到我遇到了 [spf-vim][1]，里面有许多的配置。虽然看起来有点臃肿，但这个配置有许多的用户（从其`issue`和`pull request`可以看出来），而且也能不定期地更新，添加插件或者更改配置以达到更合理的使用效果。其中的插件我使用得最多的是 [neocomplete][2]，不管是更改 shell 脚本还是写程序，这个插件的自动补全是用得最多的。但是这个插件有个要求，vim 必须要有 lua 支持。可 ubuntu（我在使用的 linux 发行版）提供的 vim 包是没有 lua 支持，于是只能自己去编译一个新的 vim 了。

谷歌一阵后，我发现有许多人给出了编译过程，并且许多人是用最新的打了补丁的 vim 的源码，而并非 [vim 官网][3] 发布的正式版。至于原因，用过就知道了。可我面临一个问题，如何从 [vim 的源码仓库][4] 里拉来最新的源码？于是又是一阵的翻墙搜索，找寻可靠的翻墙手段，最后是用了 [greate agent][5]，不过可惜的是现在这个已经没了 Linux 版本。我把自己现在还在用的 linux 版本放到了自己的 [github 库][6] 里。

---

拉来源码后，就开始了编译，选定一大堆选项，进行配置
{% highlight sh %}
./configure --prefix=/home/vagrant/tools/vim --enable-pythoninterp --enable-rubyinterp=dynamic --enable-tclinterp --enable-perlinterp --enable-luainterp --with-features=huge --with-compiledby="gisphm <phmfk@hotmail.com>" --enable-multibyte --enable-sniff --enable-cscope --disable-gpm --without-x   --disable-gui --disable-netbeans
{% endhighlight %}

配置之后就是`make`，然后安装，简单的 vim 就完成了。

---

`vim --version` 输出为
{% highlight sh linenos %}
Huge version without GUI.  Features included (+) or not (-):
+acl             +farsi           +mouse_netterm   +syntax
+arabic          +file_in_path    +mouse_sgr       +tag_binary
+autocmd         +find_in_path    -mouse_sysmouse  +tag_old_static
-balloon_eval    +float           +mouse_urxvt     -tag_any_white
-browse          +folding         +mouse_xterm     +tcl
++builtin_terms  -footer          +multi_byte      +terminfo
+byte_offset     +fork()          +multi_lang      +termresponse
+cindent         +gettext         -mzscheme        +textobjects
-clientserver    -hangul_input    -netbeans_intg   +title
-clipboard       +iconv           +path_extra      -toolbar
+cmdline_compl   +insert_expand   +perl            +user_commands
+cmdline_hist    +jumplist        +persistent_undo +vertsplit
+cmdline_info    +keymap          +postscript      +virtualedit
+comments        +langmap         +printer         +visual
+conceal         +libcall         +profile         +visualextra
+cryptv          +linebreak       +python          +viminfo
+cscope          +lispindent      -python3         +vreplace
+cursorbind      +listcmds        +quickfix        +wildignore
+cursorshape     +localmap        +reltime         +wildmenu
+dialog_con      +lua             +rightleft       +windows
+diff            +menu            +ruby/dyn        +writebackup
+digraphs        +mksession       +scrollbind      -X11
-dnd             +modify_fname    +signs           -xfontset
-ebcdic          +mouse           +smartindent     -xim
+emacs_tags      -mouseshape      +sniff           -xsmp
+eval            +mouse_dec       +startuptime     -xterm_clipboard
+ex_extra        -mouse_gpm       +statusline      -xterm_save
+extra_search    -mouse_jsbterm   -sun_workshop    -xpm
   system vimrc file: "$VIM/vimrc"
     user vimrc file: "$HOME/.vimrc"
 2nd user vimrc file: "~/.vim/vimrc"
      user exrc file: "$HOME/.exrc"
  fall-back for $VIM: "/home/vagrant/tools/vim/share/vim"
 f-b for $VIMRUNTIME: "/home/vagrant/tools/vim/share/vim/vim74"
Compilation: gcc -c -I. -Iproto -DHAVE_CONFIG_H     -g -O2 -U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=1     -I/usr/include/tcl8.6  -D_REENTRANT=1  -D_THREAD_SAFE=1  -D_LARGEFILE64_SOURCE=1
Linking: gcc   -L. -fstack-protector -rdynamic -Wl,-export-dynamic -Wl,-E   -L/usr/local/lib -Wl,--as-needed -o vim        -lm -ltinfo  -lselinux  -lacl -lattr -ldl  -L/usr/lib -llua5.2 -Wl,-E  -fstack-protector -L/usr/local/lib  -L/usr/lib/perl/5.18/CORE -lperl -ldl -lm -lpthread -lcrypt -L/home/vagrant/.pyenv/versions/2.7.9/lib/python2.7/config -lpython2.7 -lpthread -ldl -lutil -lm -Xlinker -export-dynamic  -L/usr/lib/x86_64-linux-gnu -ltcl8.6 -ldl -lz -lpthread -lieee -lm
{% endhighlight %}

---

为了方便，我把 [vim 的官方源码仓库][4] 镜像了一份放到[自己的 github 仓库上][7]。同时我在 windows 平台上用 vs2010 编译了 [64 位的 vim][8]，具备 lua 支持。

---

[1]: https://github.com/spf13/spf13-vim
[2]: https://github.com/Shougo/neocomplete.vim
[3]: http://www.vim.org
[4]: https://code.google.com/p/vim
[5]: https://github.com/greatagent/greatagent
[6]: https://github.com/gisphm/wp-linux
[7]: https://github.com/gisphm/vim-mirror
[8]: https://github.com/gisphm/vimx64
