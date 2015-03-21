---
layout: post
title: 学习Rails中遇到的问题一
---

## 概述
早想学习Rails，但却奈于时间限制，一直没有去动。现在终于有了整块的时间，可以慢慢来看看了。

顺便花了点RMB买了本安道翻译的《Ruby on Rails教程》，对照着[官网][1]的英文版一起学习这个框架。

这里主要把一些学习中遇到的问题记录下来。

## 问题一
### 描述

第三章的`rake test`运行后出错，错误信息如下：

```
$HOME/.rvm/gems/ruby-2.2.1/gems/activesupport-4.2.1/lib/active_support/dependencies.rb:274:in `require': cannot load such file -- guard (LoadError)
	from $HOME/.rvm/gems/ruby-2.2.1/gems/activesupport-4.2.1/lib/active_support/dependencies.rb:274:in `block in require'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/activesupport-4.2.1/lib/active_support/dependencies.rb:240:in `load_dependency'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/activesupport-4.2.1/lib/active_support/dependencies.rb:274:in `require'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/guard-minitest-2.4.4/lib/minitest/guard_minitest_plugin.rb:4:in `<top (required)>'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/activesupport-4.2.1/lib/active_support/dependencies.rb:274:in `require'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/activesupport-4.2.1/lib/active_support/dependencies.rb:274:in `block in require'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/activesupport-4.2.1/lib/active_support/dependencies.rb:240:in `load_dependency'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/activesupport-4.2.1/lib/active_support/dependencies.rb:274:in `require'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/minitest-5.5.1/lib/minitest.rb:91:in `block in load_plugins'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/minitest-5.5.1/lib/minitest.rb:85:in `each'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/minitest-5.5.1/lib/minitest.rb:85:in `load_plugins'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/minitest-5.5.1/lib/minitest.rb:114:in `run'
	from $HOME/.rvm/gems/ruby-2.2.1/gems/minitest-5.5.1/lib/minitest.rb:56:in `block in autorun'
	from $HOME/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in `require'
	from $HOME/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in `require'
	from -e:1:in `<main>'
```

原书里也没有针对这个的解，谷歌一阵，结果啥都没有，郁闷了一下。主要是自己对ruby也不是很熟悉。

### 解决
不甘心就这么断在这里，仔细看错误信息是说`LoadErorr`，即`guard`载入错误。可我一检查`Gemfile.lock`，没这个gem。

好吧，把这个gem加入Gemfile的合适位置。然后`bundle install`，再运行`rake test`，就算是解决了，输出如下

```
Minitest::UnexpectedError: ActionController::UrlGenerationError: No route matches {:action=>"about", :controller=>"static_pages"}
    test/controllers/static_pages_controller_test.rb:15:in `block in <class:StaticPagesControllerTest>'
test/controllers/static_pages_controller_test.rb:15:in `block in <class:StaticPagesControllerTest>'
Finished in 0.23822s
3 tests, 2 assertions, 0 failures, 1 errors, 0 skips
```


[1]: https://www.railstutorial.org