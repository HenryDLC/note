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
建立密码验证插件
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD PLUGIN can be used to test passwords and improve security. It checks the strength of password and allows the users to set only those passwords which are secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No: y 
选择密码规则
There are three levels of password validation policy:

LOW    Length >= 8
#长度大于等于8
MEDIUM Length >= 8, numeric, mixed case, and special characters
#长度大于等于8，数字、大小写字母、特殊符号
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file
#长度大于等于8，数字、大小写字母、特殊符号和字典文件（慎选！）

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
Please set the password for root here.

New password: （输入你的密码）
Re-enter new password: （再次输入你的密码）
