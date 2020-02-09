[TOC]

# 五、Linux压缩命令

### 1、常见的压缩格式

- 常用压缩格式：.zip  .gz  .bz2
- **常见压缩格式： tae.gz   tar.bz2**  ( 最常用 )

#### .zip 格式

#### 1.1 压缩命令：

- zip 压缩文件名 源文件  (.zip格式与Windows一样的格式)
  - 压缩文件

如： zip  longzls.zip longzls

- zip -r 压缩文件名  源目录
  - 压缩目录

#### 1.2 解压缩

- unzip 压缩文件

####.gz格式

#### 1.3 压缩命令

- gzip 源文件
  - 压缩为.gz格式的压缩文件，源文件会消失
- gzip -r 源文件 > 压缩文件
  - 压缩为.gz格式，源文件保留
  - 例如：  gzip -c cangls > cangls.gz
- gzip -r 目录
  - 压缩目录下所有的**子文件**，但是不能压缩目录

### [输出重定向命令 ： > ]

#### 1.4 解压命令

- gzip -d 压缩文件
  - 解压缩文件
- gunizp 压缩文件
  - 解压缩文件

### 2、打包命令

#### 2.1 打包与解打包

- tar -cvf 打包文件名  源文件
  - -c : 打包
  - -v : 显示过程
  - -f : 指定打包后的文件名
- 例如： tar -cvf langzls.tar  langzls
- tar -xvf 打包文件名
  - -x : 解打包
- 例如：tar -xvf longzls.tar

####  2.2 .tar.gz压缩格式

其实，.tar.gz 格式就是先打包为.tar格式，再压缩为.gz格式

- tar -zcvf   压缩包名为.tzr.gz   源文件
  - -z ： 压缩为.tar.gz格式
- tar -zxvf   压缩包名
  - -x : 解压缩.tar.gz格式

#### 2.3 .ta.bz2 压缩格式

- tar -jcvf 压缩包名.tar.bz2 源文件
  - -z  :  压缩为.tar.bz2格式
- tar -jxvf  压缩包名.tar.gz2
  - -x ： 解压缩.tar.bz2格式

#### 2.4 解压缩到指定文件

- tar  -zxvf   abc.tar.gz   -C   ../
  - 加-C  后面接指定文件目录

2.5 压缩多个文件

- tar   -zcvf   ../test.tar.gz abc.    abc.txt   japan
  - 把多个文件放在目标压缩文件后面

#### 2.6 只查看压缩目录下的文件，而不解压

- tar -ztvf  abc.tar.gz