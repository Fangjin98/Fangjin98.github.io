# My Blog

This branch contains the source codes of [my blog](https://www.fangjin.site/). To develop run 

```shell
git clone --recursive -b source https://github.com/Fangjin98/Fangjin98.github.io.git 
```

or you can update submodule later

```shell
git clone -b source https://github.com/Fangjin98/Fangjin98.github.io.git blog
cd blog
git submodule update --init
```

This blog is based on [Hexo](https://hexo.io/zh-cn/index.html) and a fork of [Minima](https://github.com/Fangjin98/hexo-theme-minima). After cloning the repo, run

```shell
npm install --force
hexo g && hexo s
```
