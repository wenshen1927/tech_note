#mybatis多表查询

![image-20190809230726493](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190809230726493.png)

示例：用户和账户

​		一个用户可以有多个账户

​		一个账户只能属于一个用户(多个账户也可以属于一个用户）

建表：

​	1、用户表，账户表

​		让用户表和账户表之间具备一对多的关系：需要使用外间在账户表中添加

​	2、两个实体类：用户实体类，账户实体类

​		让用户和账户的实体类能体现出一对多的关系

​	3、建立两个配置文件

​		用户的配置文件

​		账户的配置文件

​	4、实现配置：

​		当我们查询用户时，可以同时得到用户下所包含的账户信息；

​		当我们查询账户时，可以同时得到账户的所属用户信息