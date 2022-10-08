#### 一、Linux文件权限

##### 1. Linux文件属性

![image-20221008202431406](/Users/berry/Library/Application Support/typora-user-images/image-20221008202431406.png)

1.1 第一部分为文件的类型与权限：

- 第一个字符为文件类型：[d]表示目录、[-]表示文件、[l]表示链接文件、[b]表示设备文件里面的可供存储的周边设备、[c]表示设备文件里的序列埠设备；
- 后面的字符三个为一组，第一组为文件拥有者可具备的权限，第二组为加入此群组的账号的权限，第三组为非本人且没有加入本群组的其他账号的权限，每一组的第一个字符表示是否可读[r]，每一组的第二个字符表示是否可写[w]，每一组的第三个字符表示是否可执行[x]；

1.2 第二部分表示有多少文件名链接到此节点；

1.3 第三部分表示这个文件或目录的拥有者账号；

1.4 第四部分表示这个文件的所属群组；

1.5 第五部分表示这个文件的容量大小，单位为Bytes；

1.6 第六部分为这个文件的创建日期或最近的修改日期，如果未变动时间太久则只显示年份；

1.7 第七部分为这个文件的文件名，文件名前有一个[.]为隐藏文件；

##### 2. 修改文件属性与权限

2.1 改变所属劝阻，chgrp

```bash
chgrp user1 test.txt #第二个字段为群组名，需在etc/group文件中，最后一个字段为文件名
```

2.2 改变文件拥有者，chown

```bash
chown user1 test.txt #第二个字段为用户名，需在etc/passwd文件中，最后一个字段为文件名
```

```bash
chown user1:user1 text.txt #同时改变群组
chown user1.user1 text.txt
```

```bash
chown .user1 text.txt #只改群组
chown :user1 text.txt
```

-R：进行递回的持续变更，亦即连同次目录下的所有文件都变更。

2.3 改变权限，chmod

- 数字类型改变文件权限，r对应为4，w对应为2，x对应为1

```bash
chmod 777 test.txt #第二个字段中的每个数字对应为owner/group/other各自的rwx的累加，后面接文件名
```

- 符号类型改变文件权限，user对u，group对应g，other对应o，a对应all所有身份，可以使用+、-、=来操作权限rwx

```bash
chmod u=rwx,go=rx text.txt #第二个字段设置权限，后接文件名
chmod a+x test.txt
chmod a-x test.txt
```



