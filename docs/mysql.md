## 用户(user)

select host, user, authentication_string, plugin from user;

主机 user 认证string plugin

## 主机
mysql的%虽然表示是任何主机，但是它只是针对于通过TCP/IP连接过来的主机。类似于mysql -h 172.16.0.3这种。 
另外还有两种：

1、localhost

2、127.0.0.1 
%不能替代上面两种，也就是说，你在本机用mysql -hlocalhost（等同于mysql 不指定-h)，mysql -h127.0.0.1方式连接数据库，MySQL的权限验证模块都会采用不同的方式。

## 修改mysql plugin
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'

ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '1';

Don't forget to `flush privileges`;
