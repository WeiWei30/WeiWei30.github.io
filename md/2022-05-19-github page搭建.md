---
layout: post
category: 计算机
---

## 远程构建github pages

远程构建是通过建造仓库，利用github自动构建网页。优势在于不用在本地安装各种构建的软件，缺点是不是real-time的，修改后需要等待很长时间才能在网页上体现。所以推荐的方法是：在[本地修改好网页](## 本地构建github pages)后，git到仓库release更新的网页。

如果想从头搭建一个网页，创建一个`USER_NAME.github.io`的仓库，设为public，github会自动生成网页，地址为 USER_NAME.github.io。

如果想用别人的模板，直接Fork别人的仓库，然后重命名为`USER_NAME.github.io`即可。

## 本地构建github pages

本地构建需要使用`jekyll`，详细步骤可以参考[官方教程](https://docs.github.com/cn/pages/setting-up-a-github-pages-site-with-jekyll)。这里主要记录一下安装`jekyll`过程中的坑。

`jekyll`是使用`Ruby`编写的静态网页生成器，所以需要先安装`Ruby`。Mac系统自带了`Ruby`语言，但版本低，所以需要安装更高版本的，并且覆盖Mac自带的。可以参考[这篇文档](https://onblogs.net/_posts/2020/2020-02-10-Mac%E4%B8%8A%E4%BD%BF%E7%94%A8brew%E5%8F%A6%E8%A3%85ruby%E5%92%8Cgem%E7%9A%84%E6%96%B0%E7%8E%A9%E6%B3%95/)，主要需要注意的是将自行安装的 ruby 添加到环境变量中，并保证优先级大于系统自带的 ruby。

之后再使用`gem install bundler`安装`bundler`。

使用`jekyll`创建站点：

```bash
jekyll new Folder_name --skip-bundle
```

根据需求通过`bunlder`安装依赖项：

```bash
bundle install
```

最后使用`jekyll`在本地测试站点：

```bash
bundle exec jekyll serve --watch
```





