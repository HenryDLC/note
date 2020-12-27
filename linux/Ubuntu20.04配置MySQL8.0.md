Ubuntu20.04配置MySQL8.0
sudo apt-get update #更新源
sudo apt-get install mysql-server #安装mysql
sudo mysql_secure_installation #按提示设置即可
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf #找到 bind-address 修改值为 0.0.0.0(如果需要远程访问)
sudo /etc/init.d/mysql restart #重启mysql