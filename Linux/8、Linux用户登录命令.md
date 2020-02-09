[TOC]

#八、Linux用户登录命令

##1、查看登录用户信息

###w 用户名

![image-20190906223123573](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906223123573.png)

​	第一行：系统时间  登录时间 负载：1min,5min,15min

![image-20190906223316379](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906223316379.png)	

###who 

- 只能看到 用户名  登录终端  登录时间

###last 

- 查询当前登录和过去登录的用户信息(查看所有用户的登录信息)

  ![image-20190906223455677](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906223455677.png)

- 实际上是读取文件 /var/log/wtmp文件，但是该文件只能用这个命令查看，不可以修改

###lastlog 

- 查看所有用户的最后一次登录时间

![image-20190906223747127](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906223747127.png)

实际也是差文件，且该文件不可修改