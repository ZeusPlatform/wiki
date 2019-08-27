docker pull mysql

docker container rm mysql

docker run --rm --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1 -d mysql

docker exec -it mysql bash

mysql -uroot -p -h localhost #输入密码

grant all PRIVILEGES on .* to root@'%' WITH GRANT OPTION;

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'

docker inspect --format='{{.Name}} - {{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $(docker ps -aq)
查看容器ip

获取所有容器名称及其ip地址
`docker inspect -f '{{.Name}} - {{.NetworkSettings.IPAddress }}' $(docker ps -aq)`

### mysql 8 的node mysql连接问题
docker exec -it YOUR_CONTAINER mysql -u root -p
Enter password:
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '{your password}';
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '{your password}';
SELECT plugin FROM mysql.user WHERE User = 'root';