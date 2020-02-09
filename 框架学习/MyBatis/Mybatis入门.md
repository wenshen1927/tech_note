

#Mybatis入门

[TOC]

大纲：

- mybatis概述
- mybatis环境搭建
- mybatis入门案例
- 自定义mybatis框架

####1、框架

​	框架是软件开发中的一套解决方案，不同的框架解决不同的问题。

​	框架封装了很多细节，使开发者可以用简单的方式实现功能，提高开发效率。

####2、三层架构

![image-20190728233232173](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190728233232173.png)

表现层：展示数据

业务层：处理业务需求

持久层：和数据库交互

####3、持久层技术解决方案

- JDBC技术：
  - Connection
  - PreparedStatement
  - ResultSet
- Spring的JdbcTemplate
  - Spring对JDBC的简单封装
- Apache的DBUtiles：
  - 对JDBC的简单封装

JDBC是规范，其余两个是工具类（仅仅是简单的封装），算不上框架。

####4、Mybatis框架

- 一个优秀的Java持久层框架，内部封装了JDBC，使开发者==只关注SQL语句本身==，而不需要花费精力去处理驱动加载，创建连接，创建statement等复杂操作。
- 通过xml或注解配置Statement
- 使用ORM思想实现结果集的封装
  - ORM就是把数据表的实体类和实体类的属性对应起来，让我们通过操作能够实体类就可以操纵数据库表
  - 数据库表中的字段名和实体类的属性名保持一致

####5、mybatis入门

- 环境搭建

  - ==第一步：创建maven工程，并导入坐标==

  - ==第二步：创建实体类（bean）和dao的接口==

  - ==第三步：创建Mybatis的主配置文件，配置数据库相关环境==

    ​		      	==SqlMapCongfig.xml==

    ![image-20190805235238300](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190805235238300.png)

  - ==第四部：创建映射配置文件==
    				==IUserDao.xml==

    ![image-20190805235337908](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190805235337908.png)

- 环境搭建的注意事项

  - 第一个：创建IUserDao.xml 和 IUserDao.java时名称是为了和我们之前的知识保持一致。
    		在Mybatis中它把持久层的操作接口名称和映射文件也叫做：Mapper
    		所以：IUserDao 和 IUserMapper是一样的

  - 第二个：在idea中创建目录的时候，它和包是不一样的
    		包在创建时：com.itheima.dao它是三级结构
    		目录在创建时：com.itheima.dao是一级目录

    ​		(注：这一条在mac下面不成立，用.分隔的文件属于不同级别的目录，可能在win环境下这条成立，待验证)

  - ==第三个==：mybatis的映射配置文件位置必须和dao接口的包结构相同

  - ==第四个==：映射配置文件的mapper标签namespace属性的取值必须是dao接口的全限定类名

  - ==第五个==：映射配置文件的操作配置（select），id属性的取值必须是dao接口的方法名

  - ==当我们遵从了第三，四，五点之后，我们在开发中就无须再写dao的实现类==。

- 分析一下mybatis实现类的细节：

  - mybatis的入门案例
    		第一步：读取配置文件
    		第二步：创建SqlSessionFactory工厂
    		第三步：创建SqlSession
    		第四步：创建Dao接口的代理对象
    		第五步：执行dao中的方法
    		第六步：释放资源

    		注意事项：
    			不要忘记在映射配置（IUserDao.xml）中告知mybatis要封装到哪个实体类中(如resultType="User")
    			配置的方式：指定实体类的全限定类名

<img src="/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190729235237658.png" style="height:350px;width:1000px" >

```java
//1.读取配置文件
InputStream in = Resources.getResourceAsStream("SqlMapConfig.xml");//如果路径出问题怎么办？
//2.创建SqlSessionFactory工厂
SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();//这是个什么玩意？为啥不直接new SqlSessionFactory的实现类，而要用这个builder来创建呢？  答：构建者模式
SqlSessionFactory factory = builder.build(in);//mydatis把读取文件，加载配置，创建工厂类的步骤全部封装起来
//3.使用工厂创建SqlSession对象
SqlSession sqlSession = factory.openSession();//工厂模式创建sqlSession，解耦，当创建新的子类的时候，不需要改变源码
//4.使用SqlSession创建Dao接口的代理对象mapper （代理模式：在不改变源码的基础上，对类进行增强）
IUserDao mapper = sqlSession.getMapper(IUserDao.class);
//5.使用代理对象执行方法
List<User> users = mapper.findAll();
for (User user : users) {
    System.out.println(user);
}
//6.释放资源
sqlSession.close();
in.close();
```

- mybatis基于注解的入门案例：]
  			把IUserDao.xml移除，在dao接口的方法上使用@Select注解，并且指定SQL语句
  			同时需要在SqlMapConfig.xml中的mapper配置时，使用class属性指定dao接口的全限定类名。
  	明确：
  		我们在实际开发中，都是越简便越好，所以都是采用不写dao实现类的方式，不管使用XML还是注解配置。
  		但是Mybatis它是支持写dao实现类的。



####6、自定义Mybatis的分析：

​		mybatis在使用代理dao的方式实现增删改查时做什么事？

​			两件事：第一：创建代理对象

​				       第二：在代理对象中调用selectList()

知识点：工厂模式，构建者模式，代理模式，反射，自定义注解，注解的反射，xml解析，数据库元数据，元数据的反射等。

​		分析一下配置文件的流程 ：

![image-20190807000828120](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190807000828120.png)

![image-20190807001329529](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190807001329529.png)

![image-20190807001459298](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190807001459298.png)

​	

自定义mybatis能通过入门案例看到的类：

​		class Resource

​		class SqlSessionFactoryBuilder

​		interface SqlSessionFactory

​		interface SqlSession