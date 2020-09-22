---
title: 常用shell命令
---

# 常用shell命令

## du(dask usage) 命令详解

```shell
du [-abcDhHklmsSx][-L <符号连接>][-X <文件>][--block-size][--exclude=<目录或文件>][--max-depth=<目录层数>][--help][--version][目录或文件]
```

* `-a` 或 `-all` 显示全部文件大小
* `-b`或`-bytes`  显示目录或文件大小时，以byte为单位。
* `-h`或`-human-readable`  以K，M，G为单位，提高信息的可读性。
* `-H`或`--si`  与`-h`参数相同，但是K，M，G是以1000为换算单位。
* `-s`或`--summarize`  仅显示总计。
* `-S`或`--separate-dirs`  显示个别目录的大小时，并不含其子目录的大小。
* ` -X`<文件>或`--exclude-from=<文件>`  在<文件>指定目录或文件。
* `--exclude=<目录或文件>`  略过指定的目录或文件。
* `--max-depth=<目录层数>`  超过指定层数的目录后，予以忽略。

## man - an interface to the on-line reference manuals(命令在线参考)

```bash
# 查看pwd命令详情
man pwd
```

- 按`h`获取帮助，按`q`推出

  

## lsblk - list block devices(磁盘清单)



```ba
[root@server-mom-test ~]# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
fd0               2:0    1    4K  0 disk 
sda               8:0    0   50G  0 disk 
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   49G  0 part 
  ├─centos-root 253:0    0  244G  0 lvm  /
  └─centos-swap 253:1    0    5G  0 lvm  [SWAP]
sdb               8:16   0  200G  0 disk 
└─sdb1            8:17   0  200G  0 part 
  └─centos-root 253:0    0  244G  0 lvm  /
sr0              11:0    1 1024M  0 rom  
```



##  fdisk - manipulate disk partition table(操作磁盘分区表)



```bash
[root@server-mom-test ~]# fdisk /dev/sdb
欢迎使用 fdisk (util-linux 2.23.2)。

更改将停留在内存中，直到您决定将更改写入磁盘。
使用写入命令前请三思。

命令(输入 m 获取帮助)：n
Partition type:
   p   primary (1 primary, 0 extended, 3 free)
   e   extended
Select (default p): p
分区号 (1-4，默认 1)：
起始 扇区 (2048-10485759，默认为 2048)：
将使用默认值 2048
Last 扇区, +扇区 or +size{K,M,G} (2048-10485759，默认为 10485759)：
将使用默认值 10485759
分区 1 已设置为 Linux 类型，大小设为 5 GiB

命令(输入 m 获取帮助)：w
The partition table has been altered!

Calling ioctl() to re-read partition table.
正在同步磁盘。

```



## lvm -  LVM2 tools(创建物理卷)



```bash
lvm> pvcreate /dev/sdb
  Physical volume "/dev/sdb" successfully created.
lvm> pvdisplay
  --- Physical volume ---
  PV Name               /dev/sda2
```



## 利用ssh传输文件 scp(secure copy (remote file copy program))



在linux下一般用scp这个命令来通过ssh传输文件。

* -P(port)指定端口号。(Specifies the port to connect to on the remote host.  Note that this option is written with a capital ‘P’, because -p is already reserved for preserving the times and modes  of the file.)
* -l(limit) Limits the used bandwidth, specified in Kbit/s.

1. 从服务器上下载文件

```bash
# scp root@192.168.0.101:/var/www/test.txt 把192.168.0.101上的/var/www/test.txt 的文件下载到/var/www/local_dir
$ scp username@servername:/path/filename /var/www/local_dir
```

2. 上传本地文件到服务器

```bash
$ scp /path/filename username@servername:/path  
```

3. 从服务器下载整个目录

```bash
# 递归的下载整个目录
$ scp -r username@servername:/var/www/remote_dir/ /var/www/local_dir
```

4. 上传目录到服务器

```bash
$ scp -r local_dir username@servername:remote_dir
```



## free - 显示系统中已用和未用的内存空间总和

总览 (SYNOPSIS)
       free [-b | -k | -m] [-o] [-s delay ] [-t] [-V]

描述 (DESCRIPTION)
       free 显示 系统中 已用和未用的 物理内存和交换内存, 共享内存和 内核使用的 缓冲区的 总和.

选项 (Options)

       -b 选项 以字节为单位 显示 内存总和; -k 选项 (缺省的) 以 KB 为单位 显示; -m 选项 以 MB 为单位.
       
       -t 选项 显示 一个 总计行.
       
       -h 选项 以M，G显示
    
       -o 选项 禁止 "buffer adjusted" 行的显示. 除非 指定 free 从 (相应的) 已用/未用的 内存 减去/加上 缓冲区内存.
    
       -s 使 free 以 delay 秒为间隔, 连续抽样显示. delay 可以设置成浮点数, 它用 usleep(3) 做 微秒级 延迟.
    
       -V 显示版本信息.