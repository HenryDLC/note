ubuntu:~$ vim ~/.profile
> 添加下面内容
export LANG="zh_CN.UTF-8"
export LC_ALL="zh_CN.UTF-8"

>出现错误，说明没有安装zh_CN.UTF-8语言。
安装:`sudo locale-gen zh_CN.UTF-8`
> ubuntu:~$ locale