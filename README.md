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

This blog is based on Hexo and a fork of Minima. After cloning the repo, run

```shell
npm install --force
hexo g && hexo s
```
