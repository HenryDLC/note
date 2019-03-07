# 更改添加系统UTF-8中文
ubuntu:~$ vim ~/.profile
> 添加下面内容
export LANG="zh_CN.UTF-8"
export LC_ALL="zh_CN.UTF-8"
> 查看当前系统已安装的语言
ubuntu:~$ locale -a
出现错误，说明没有安装zh_CN.UTF-8语言。
安装:`sudo locale-gen zh_CN.UTF-8`
ubuntu:~$ > locale

# ubuntu增加交换空间
> sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo "/swapfile none swap sw 0 0" | sudo tee -a /etc/fstab