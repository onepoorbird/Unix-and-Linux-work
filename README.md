# Unix-and-Linux-work
This is some Linux code to complete the task assigned by my teacher Ms.Cheng.

# Introduction
Build a file system through Linux to implement operations such as adding, deleting, modifying and checking.

# Requirements
- VMware work station
- Ubuntu 20/22/24 (these are all ok)

# Run the code
First,you must install some tools to compile the c.

Then,open your terminal and enter the path your code exist.

Run the code following to compile the filesys.c file into an executable file and then run it:
```bash
gcc -o a.out filesys.c 
./a.out
```

# Futrue
1. 目录操作的边界处理不完善
<img width="404" alt="image" src="https://github.com/user-attachments/assets/b7cfe1ef-875e-4c6b-bf72-cb55fc21b2bb" />

可增加父目录判断语句，同时若没有控fcb需要返回错误并提示用户

2. 不支持多级目录的递归操作

不能实现以下类似的操作
```bash
my_mkdir a/b/c/d和my_create a/b/c/d/hello.txt
```
3. 非空目录能否删除要进行提示

<img width="388" alt="image" src="https://github.com/user-attachments/assets/e625846d-ac82-4f72-b866-2fe18a90e45e" />

实际系统中是可以删除的，此处代码可以对命令进行一个判断，若目录非空，可告知用户并询问是否确认删除，若确认可以进行后续操作，否则return。

4. 创建目录和文件时的命名提示

没有添加对于创建目录和文件时的命名提示语句，如命名规则要求长度在20个字节以内。命名长度具体可以在init.h里面进行修改。

5. do_write操作失败的处理

在do_write中，如果写入过程中磁盘块分配失败，代码可能导致部分写入完成，剩余数据丢失，因此可以实现事务机制，确保写入失败时回滚所有修改。

6. 创建新的空闲磁盘块的性能提升方法

在get_free_block中，本代码使用线性扫描寻找空闲块，在磁盘空间较大时效率低。

<img width="364" alt="image" src="https://github.com/user-attachments/assets/2d688ae6-b096-49ea-9b25-9d131b7ab075" />

此时若使用链表管理空闲块，不需要便利整个链表，直接从头指针取或者位图。

7.控制台语句显示冗余

<img width="225" alt="image" src="https://github.com/user-attachments/assets/cdc7a9f9-83cc-443a-b23c-f53f3d136020" />

在打开文件后，语句前缀不应该出现1.txt命令，这与实际的linux操作面板不符。
