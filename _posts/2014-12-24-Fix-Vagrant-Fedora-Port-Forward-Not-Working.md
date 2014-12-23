---
layout: post
title: 解决vagrant的fedora box里端口映射的问题
---

### 概述
问题其实比较简单的，主要是解决的方法是相当简单的。

### 问题产生
问题源起我用烦了ubuntu的box，总感觉各种库略旧，vivid又还只是alpha，肯定会有坑。于是我就选择了fedora 21的server版本。恰好谷歌一会后，发现vagrant cloud上已经[有人][1]做了box，于是直接下载来用。

夜晚的网络比较稳定高速，安装也是一路顺利。可等到我把自己的github pages给clone下来后，想在本地看看能否查看，结果运行下面命令后，`jekyll serve --watch`，在主机的浏览器里怎么也看不到网页的出现。问题也就产生了，端口映射出问题了。

### 寻找答案
谷歌一下，最先找到的是说iptables。可我运行`sudo systemctl status iptables.service` 发现，这服务`dead`了。压根没它什么事。

然后再找，说是fedora的防火墙，`firewalld.service`。结果我一查，确实是开着。开发的机器不需要什么防火墙，至少我是这么认为的。于是，干掉防火墙——`sudo systemctl disable firewalld.service`。可在主机里问题仍旧。

最后，找到了一种可能的答案，把vagrant的启动过程debug一下。我一想，这日志输出有点恐怖，不能这么做。对于vagrant，我装了插件[vagrant-vbguest][2]。于是我试试把vbguest的检查更新选项打开。
{% highlight ruby %}
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vbguest.auto_update=true

end
{% endhighlight %}
结果问题就很明显了，启动时的控制台输出表明虚拟机的vbox相关服务出问题了。于是，我就去寻找虚拟机里的vbox相关服务与软件包的安装情况。因为在更新时我发现，内核有更新，但vbox相关的kmod却没有，问题估计会出现在软件包上。

### 解决
一查，`vboxservice.service`启动失败（`failed`），所报的错误，网上也没有解决办法。于是，我尝试从软件包问题上进行解决。fedora最麻烦的一点是，像virtualbox、音视频解码等一些软件包自己不维护，或者说因为许可证什么的自己不去搞，让使用者自行去找。

果断把`rpmfusion`的两个包下回来，直接`sudo yum localinstall`之，把这个仓库激活。`yum makecache`建立元数据缓存，查找`VirtualBox`，就找到了未随内核升级的`kmod-virtualbox`模块。于是就简单了，安装缺失的软件包，重启`vboxservice.service`。

在主机的cmd里输入`vagrant vbguest --status`，输出的结果是`GuestAdditions 4.3.20 running --- OK.`，证明端口映射方面已经不是问题。再运行`jekyll serve --watch`，在主机里就不会有问题了！


[1]: https://vagrantcloud.com/hansode/boxes/fedora-21-server-x86_64
[2]: https://github.com/dotless-de/vagrant-vbguest
