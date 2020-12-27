Ubuntu20.04配置MySQL8.0
sudo apt-get update #更新源
sudo apt-get install mysql-server #安装mysql
一、安装MySQL
sudo mysql_secure_installation #按提示设置即可
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf #找到 bind-address 修改值为 0.0.0.0(如果需要远程访问)
sudo /etc/init.d/mysql restart #重启mysql
二、设置root账号为远程访问
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER; #修改加密规则
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码'; #使用mysql_native_password重新修改密码
mysql> UPDATE mysql.user SET host = '%' WHERE user = 'root'; #允许远程访问
mysql> FLUSH PRIVILEGES;
三、新增用户赋权并设置远程访问
mysql> CREATE USER 'sammy'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'%' WITH GRANT OPTION;

卸载MySQL8.0
首先在终端中查看MySQL的依赖项：
dpkg --list|grep mysql
卸载：
sudo apt-get remove mysql-common
sudo apt-get autoremove --purge mysql-server-8.0
清除残留数据：dpkg -l|grep ^rc|awk ‘{print$2}’|sudo xargs dpkg -P
查看剩余依赖
dpkg --list|grep mysql
继续删除剩余依赖项，
如：sudo apt-get autoremove --purge mysql-apt-config

安全设置向导mysql_secure_installation
