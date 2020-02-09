[TOC]

# Linux用户及文件权限管理

##1、Linux中创建、删除用户，及用户组等操作

###1.1 创建用户

####root用户：

在 Linux 系统里， `root` 账户拥有整个系统至高无上的权利，比如 新建/添加 用户。

> root 权限，系统权限的一种，与 SYSTEM 权限可以理解成一个概念，但高于 Administrator 权限，root 是 Linux 和 UNIX 系统中的超级管理员用户帐户，该帐户拥有整个系统至高无上的权力，所有对象他都可以操作，所以很多黑客在入侵系统的时候，都要把权限提升到 root 权限，用 Windows 的方法理解也就是将自己的非法帐户添加到 Administrators 用户组。更比如安卓操作系统中（基于 Linux 内核）获得 root 权限之后就意味着已经获得了手机的最高权限，这时候你可以对手机中的任何文件（包括系统文件）执行所有增、删、改、查的操作。

我们一般登录系统时都是以普通账户的身份登录的，要创建用户需要 root 权限，这里就要用到 `sudo` 这个命令了。不过使用这个命令有两个大前提，一是你要知道当前登录用户的密码，二是当前用户必须在 `sudo` 用户组.

#### su，su- 与 sudo

**需要注意 Linux 环境下输入密码是不会显示的。**

`su <user>` 可以切换到用户 user，执行时需要输入目标用户的密码，`sudo <cmd>`可以以特权级别运行 cmd 命令，需要当前用户属于 sudo 组，且需要输入当前用户的密码。`su - <user>` 命令也是切换用户，同时环境变量也会跟着改变成目标用户的环境变量。

####创建用户:

**sudo adduser lilei**

adduser 命令需要root权限，可以添加一个用户到用户组，且在/home目录下生成用户目录

####切换用户：

**su  -l  lilei** 

####注销当前用户：

**exit**

###1.2 用户组

​	在 Linux 里面每个用户都有一个归属（用户组），用户组简单地理解就是一组用户的集合，它们共享一些资源和权限，同时拥有私有资源，就跟家的形式差不多，你的兄弟姐妹（不同的用户）属于同一个家（用户组），你们可以共同拥有这个家（共享资源），爸妈对待你们都一样（共享权限），你偶尔写写日记，其他人未经允许不能查看（私有资源和权限）。当然一个用户是可以属于多个用户组的，正如你既属于家庭，又属于学校或公司。

#### 查看自己属于什么用户组

**方式一：  **

**groups shiyanlou**

shiyanlou : shiyanlou 

​	其中冒号之前表示用户，后面表示该用户所属的用户组。这里可以看到 shiyanlou 用户属于 shiyanlou 用户组，每次新建用户如果不指定用户组的话，默认会自动创建一个与用户名相同的用户组（差不多就相当于家长的意思，或者说是老总）。默认情况下在 sudo 用户组里的可以使用 sudo 命令获得 root 权限。shiyanlou 用户也可以使用 sudo 命令，为什么这里没有显示在 sudo 用户组里呢？可以查看下 `/etc/sudoers.d/shiyanlou` 文件，我们在 `/etc/sudoers.d` 目录下创建了这个文件，从而给 shiyanlou 用户赋予了 sudo 权限：

​	**sudo cat /etc/sudoers.d/shiyanlou**

​	![image-20190906233012807](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906233012807.png)

**方式二：**

**查看 `/etc/group` 文件**

**cat /etc/group | sort**

这里 `cat` 命令用于读取指定文件的内容并打印到终端输出，后面会详细讲它的使用。 `| sort` 表示将读取的文本进行一个字典排序再输出，然后你将看到如下一堆输出，你可以在最下面看到 shiyanlou 的用户组信息：

![image-20190906233217527](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906233217527.png)

没找到，没关系，你可以使用命令过滤掉一些你不想看到的结果：

cat  /etc/group | grep -E "shiyanlou"

输出  ： ![image-20190906233407418](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906233407418.png)

/etc/group 的内容包括用户组（Group）、用户组口令、GID 及该用户组所包含的用户（User），每个用户组一条记录。格式如下：

> group_name:password:GID:user_list

你看到上面的 password 字段为一个 `x` 并不是说密码就是它，只是表示密码不可见而已。

这里需要注意，如果用户的 GID 等于用户组的 GID，那么最后一个字段 `user_list`就是空的，比如 shiyanlou 用户，在 `/etc/group` 中的 shiyanlou 用户组后面是不会显示的。lilei 用户，在 `/etc/group` 中的 lilei 用户组后面是不会显示的。

####将其他用户加入sudo用户组

​	默认情况下新创建的用户是不具有 root 权限的，也不在 sudo 用户组：![image-20190906234005697](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906234005697.png)

​	可以让其加入 sudo 用户组从而获取 root 权限。使用 `usermod` 命令可以为用户添加用户组，同样使用该命令你必需有 root 权限，你可以直接使用 root 用户为其它用户添加用户组，或者用其它已经在 sudo 用户组的用户使用 sudo 命令获取权限来执行该命令。

​	**sudo usermod -G sudo lilei**

​	![image-20190906234219936](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906234219936.png)

####删除用户

​	**sudo deluser lilei --remove-home**

![image-20190906234412903](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906234412903.png)

##2、Linux中的文件权限设置

​	< 与 2、Linux命令与文件处理命令 结合着看 >

###2.1 文件权限

​	文件权限就是文件的访问控制权限，即**哪些用户和组群可以访问文件以及可以执行什么样的操作**。

​	Unix/Linux系统是一个典型的**多用户系统**，不同的用户处于不同的地位，对文件和目录有不同的访问权限。为了保护系统的安全性，Unix/Linux系统除了对用户权限作了严格的界定外，还在用户身份认证、访问控制、传输安全、文件读写权限等方面作了周密的控制。

​	在 Unix/Linux中的每一个文件或目录都包含有访问权限，这些访问权限决定了谁能访问和如何访问这些文件和目录。

ls -l 输出：

![image-20190906234747376](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906234747376.png)

文件权限：

![image-20190906234829136](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190906234829136.png)

- 文件权限

  ​	读权限，表示你可以使用 `cat <file name>` 之类的命令来读取某个文件的内容；

  ​	写权限，表示你可以编辑和修改某个文件； 

  ​	执行权限，通常指可以运行的二进制程序文件或者脚本文件，如同 Windows 上的 `exe` 后缀的文件，不过 Linux 上不是通过文件后缀名来区分文件的类型。

  ​	你需要注意的一点是：

  ​	**一个目录同时具有读权限和执行权限才可以打开并查看内部文件，**

  ​	**而一个目录要有写权限才允许在其中创建其它文件**

  ​	这是因为目录文件实际保存着该目录里面的文件的列表等信息。

  所有者权限，这一点相信你应该明白了，至于**所属用户组权限，是指你所在的用户组中的所有其它用户对于该文件的权限，**比如，你有一个 iPad，那么这个用户组权限就决定了你的兄弟姐妹有没有权限使用它破坏它和占有它。



### 2.2 变更文件所有者

将一个文件的所有者改为另一个用户

**sudo chown [所有者用户名] [文件名]**

如： sudo chown  shiyanlou iphone6s 

### 2.3 修改文件权限

如果你有一个自己的文件不想被其他用户读、写、执行，那么就需要对文件的权限做修改，这里有两种方式：

- 二进制数字表示

  ![image-20190907000727619](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190907000727619.png)

  每个文件的三组权限（拥有者，所属用户组，其他用户，**记住这个顺序是一定的**）对应一个 " rwx "，也就是一个 “ 7 ”

  7 ： 读、写、执行

  6 ： 读、写

  4 ： 读

  2 ： 写

  1 ：执行

  0 ： 无读写执行

- 加减复制操作

  - 不喜欢用，较麻烦

   **chmod go-re iphone6s**

  `g`、`o` 还有 `u` 分别表示 group、others 和 user，`+` 和 `-` 分别表示增加和去掉相应的权限。

## 3 、adduser 和 useradd 区别

​	useradd 只创建用户，创建完了用 passwd lilei 去设置新用户的密码。adduser 会创建用户，创建目录，创建密码（提示你设置），做这一系列的操作。其实 useradd、userdel 这类操作更像是一种命令，执行完了就返回。而 adduser 更像是一种程序，需要你输入、确定等一系列操作。