## express generator
`npx express-generator --view=pug myapp`
`cd myapp``npm install ``DEBUG=myapp:* & npm start`

## 集成mysql
`npm install mysql`

## mysql信息
### 加密方式(my.ini文件)
```
#默认使用“mysql_native_password”插件认证
default_authentication_plugin=mysql_native_password
```
### 查看加密方式
`select host, user, authentication_string, plugin from user;`


## 创建表
CREATE DATABASE mydb;

## 选中表
USE mydb;

## 创建表

CREATE TABLE IF NOT EXISTS `tasks` (
  `id` int(11) NOT NULL,
  `task` varchar(200) NOT NULL,
  `status` tinyint(1) NOT NULL DEFAULT '1',
  `created_at` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP
);
 
ALTER TABLE `tasks` ADD PRIMARY KEY (`id`);
ALTER TABLE `tasks` MODIFY `id` int(11) NOT NULL AUTO_INCREMENT;

## 插入数据
INSERT INTO `tasks` (`id`, `task`, `status`, `created_at`) VALUES
(1, 'Find bugs', 1, '2016-04-10 23:50:40'),
(2, 'Review code', 1, '2016-04-10 23:50:40'),
(3, 'Fix bugs', 1, '2016-04-10 23:50:40'),
(4, 'Refactor Code', 1, '2016-04-10 23:50:40'),
(5, 'Push to prod', 1, '2016-04-10 23:50:50');