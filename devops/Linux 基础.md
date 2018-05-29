# Linux 基础
### 操作系统
主要功能：
1. 系统呼叫
2. 程序管理
3. 内存管理
4. 文件管理
5. 设备管理

### 用户组
默认的情况下，所有的系统上的账号不一般身份使用者，还有那个 root 的相 关信息， 都是记彔在/etc/passwd 这个档案内的。至二个人的密码则是记彔在/etc/shadow 这个档案 下。 此外，Linux 所有的组名都纪彔在/etc/group 内.
* chgrp :改变档案所属群组
* chown :改变档案拥有者
* chmod :改变档案的权限, SUID, SGID, SBIT 等等的特怅


1. /etc:配置文件
2. /bin:重要执行档
3. /dev:所需要的装置档案
4. /lib:执行档所需的函式库不核心所需的模块
5. /sbin:重要的系统执行文件
  这五个目彔千万不要和根目彔分开在不同的分割槽

### Linux 档案和管理
mkdir cp mv rm 
1. cat 由第一行开始显示档案内容
2. tac 从最后一行开始显示，可以看出tac是cat倒着写!
3. nl 显示的时候，顺道输出行号!
4. more 一页一页的显示档案内容
5. less 和more类似，但是比 more 更好的是，他可以往前翻页!
6. head 只看头几行
7. tail 只看尾巴几行
8. od 以二进制方式读取档案内容!

umask:
```
创建档案和目录的默认权限
档案权限是666 目录权限是777
例如umask的值是022
那创建的目录权限是755，即drwxr_xr_x.创建的档案权限是644,即-rw_r__r__

```
which:指令搜寻 在path的路径下搜索
#### 档案搜寻
whereis locate :在数据库上做查询
find:在磁盘上做搜索
### 磁盘与文件系统管理
```
superblock:记录filesystem的整体信息，包括inode/block的总量，使用量，剩余量，以及文件系统的格式与相关信息等；
inode:记录档案的属性，一个档案占用一个inode,同时记录此档案的数据所在的block号码；
block:实际记录档案的内容，若档案太大时，会占用都多个block.
df:列出文件系统的整体磁盘使用量
du:评估文件系统的磁盘使用量(常用在推估目录所占容量)
实体链接与符号链接:ln
hard link不能跨FileSystem,不能link目录
ln -s 建立软连接
```
#### 磁盘的分割，格式化，检验与挂载
```
磁盘分区fdisk
格式化mkfs
磁盘检验fsck badblocks
磁盘挂载与卸除 mount
虚拟内存swap
```
### 档案与文件系统的压缩与打包
```
gzip
zcat 则可以读取纯文本档被压缩后的压缩文件
bz2
tar
```
### Vim 编辑器
```
https://medium.com/actualize-network/how-to-learn-vim-a-four-week-plan-cd8b376a9b85
:sp 打开新窗口
[ctrl]+w+j切换窗口
```
### Bash
```
echo $PATH
""与''
变量需要子程序使用时需要使用export
unset取消变量
cmd1&&cmd2    cmd1||cmd2
wc cut grep
```
### 文字处理
```
sed  awk 正则表达式
```
### Shell Script
用test 和 [ ]来进行判断 例如：test -e .bash_profile 判断该文件是否存在
if [ ] then:
elif then:
else:
fi
shell script 的追踪与debug
### 系统信息
```
kill killall 发送信号给程序
常见的信号 1 9 15
free uname查看系统的信息
uptime
netstat
vmstat
```
系统服务
```
daemon启动的两种形式:stand_alone 与 super daemon
super damon 启动的两种模式:multi-threaded and single-threaded
启动脚本/etc/init.d/
设定开机后立即启动服务的方法
chkconfig
```