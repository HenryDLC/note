# 解决Access denied

配置:
Mysql8.0
Ubuntu20.04

step1
进入mysql
sudo mysql -uroot

step2
修改密码复杂度
set global validate_password.policy=0;
set global validate_password.length=4;

step3
修改root密码
use mysql；
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';
FLUSH PRIVILEGES;

备注:
另一种修改密码的方式:
mysqladmin -u root -p password 新密码