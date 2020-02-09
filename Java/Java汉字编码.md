# Java汉字编码

## 常见编码



**iso-8859-1 与 ASCII**

**GBK GB2312 BIG5**

**UNICODE** 



其中，iso-8859-1包含 ASCII；

GB2312 是简体中文，BIG5是繁体中文，GBK同时包含简体和繁体以及日文；

UNICODE 包括了所有的文字，无论中文，英文，藏文，法文，世界所有的文字都包含其中。

由于UNICODE 包含很多字符，所以他很大，如果所有字符都用Unicode编码，会很占用空间，所以出现了各种瘦身版如，utf-8,utf-16,utf-32等等。

##Java默认编码

Java默认的字符编码是Unicode，而String类型的编码方式是与JVM编码方式和本机操作系统默认字符集有关的 。