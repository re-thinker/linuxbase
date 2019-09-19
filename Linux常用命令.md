### 1. linux日常技巧
   - 可以通过按 Tab 键实现自动补全参数
   - 使用 ctrl-r 搜索命令行历史记录（按下按键之后，输入关键字便可以搜索，重复按下 ctrl-r 会向后查找匹配项，按下 Enter 键会执行当前匹配的命令，而按下右方向键会将匹配项放入当前行中，不会直接执行，以便做出修改）
   - 可以按下 ctrl-w 删除你键入的最后一个单词，ctrl-u 可以删除行内光标所在位置之前的内容，alt-b 和 alt-f 可以以单词为单位移动光标，ctrl-a 可以将光标移至行首，ctrl-e 可以将光标移至行尾，ctrl-k 可以删除光标至行尾的所有内容，ctrl-l 可以清屏(emacs快捷键)
   - 键入 history 查看命令行历史记录，再用 !n（n 是命令编号）就可以再次执行
   - 如果你输入命令的时候中途改了主意，按下 alt-# 在行首添加 # 把它当做注释再按下回车执行（或者依次按下 ctrl-a， #， enter）。这样做的话，之后借助命令行历史记录，你可以很方便恢复你刚才输入到一半的命令
   - 使用 nohup 或 disown 使一个后台进程持续运行
   - 使用 alias 来创建常用命令的快捷形式。例如：alias ll='ls -latr' 创建了一个新的命令别名 ll

### 2.  文件目录操作命令

   - ls  查看目录下的文件  最常用的参数有三个:-a、 -l 、–F 和 h
      ```shell
      ls -hl /opt/log
      ls -al /root
      ```
      
   - cd 进出目录
      ```shell
       cd ~/
       cd -
      ```
      
   - pwd 获取当前目录
	
   - mkdir 创建新的目录	
	  usage: mkdir [OPTION]... DIRECTORY
	  ```shell
	  mkdir /tmp/test1
	  mkdir -pv  /opt/log/test1/test2/test3 
	  ```
	
   - rmdir 删除空目录
      usage: rmdir [OPTION]... DIRECTORY.
	  ```shell
	  rmdir  /tmp/test1
	  rmdir -p /opt/log/test2/test3
	  ```
	  注：只能删除空目录，目录中有文件时，无法删除
	
   - cp 复制命令
      ```shell
      cp /opt/log/xmessage.log /opt/
      cp -r /opt/log/test1 /opt/
      ```
     
   - mv 移动目录或文件，引申的功能是给目录或文件重命名
      ```shell
      mv /opt/log/xmessage.log /opt/log/xmessage.log.bak
      ```
     
   - rm 用来删除文件的，rm命令常用的参数有三个-i,-r,-f
      ```shell
      rm /opt/log/xmesssage.log.bak
      系统会询问我们是否要删除xmesssage.log.bak 文件，敲了“y/n” 确认是否要删除xmesssage.log.bak 
      rm -r /opt/log/test1
      rm -f /op/log/test1
      ```
      注：使用rm -rf 时一定要注意确认，删除的文件无法恢复，根目录是可以直接删除的
   
   - touch 可更改文件或目录的日期时间，包括存取时间和更改时间，或创建一个不存在的文件。
     
   - cat 它的功能是显示或连结一般的ascii 文本文件

     ```shell
     cat /etc/profile
     ```

    分隔合并文件，配合split命令：
     ```shell
     split -b 30M typora-setup-x64.exe
     cat file1 file2 > typora-setup-x64.exe
     ```
   -  more、less 如果一个文本文件太长了超过一个屏幕的画面，可以more、less分屏查看，less功能更强大，支持搜索
      
   - tail、head，从尾、从头查看文件内容，常用-n选项，显示多少，tail 还有个-f命令，用于跟踪文件变化，常用于查看程序实时日志

     ```shell
     tail -f xmessage.log
     tailf xmeessage.log
     ```
     注：tail -f 经常被使用，有个独立的tailf程序
     
### 3.  文件查找命令

   - find 查找文件和目录
     usage :  find [PATH] [option] [action] 

     -name 按照文件名查找
     -perm 按照文件权限来查找文件
     -user 按照文件属性查找文件
     -group 按照文件所属的组查找文件
     -mtime -n +n 按照文件的更改时间来查找文件
     -type 查找某一类型的文件 d:目录 l:符号链接文件 f:普通文件
     -size n 查找文件长度为n块文件
     ```shell
     find ./ -name Makefile
     find ./ -perm 777
     find ./ -size +1000c 大于1k的文件
     find ./ mtime +5
     find ./ -name *.log | xargs -i mv {} /opt/log
     find / -user mongod
     ```
### 4. 文件的压缩与解压
   - tar 压缩解压tar包
     常用参数：

     -z  -gzip 压缩

     -x  -extract 解压
     -c  -create 创建文件
     -v  -verbose 生成详细输出
     -f  -file 指定归档文件名
     -C 改变目录

     ```shell
     tar -xzvf go1.12.7.linux-amd64.tar.gz -C /usr/local
     tar -czvf log.bak /opt/log
     ```
   - zip unzip zip格式文件
     ```shell
     zip file.zip /opt/log/*
     unzip file.zip -d ./test
     unzip file.zip 
     ```
### 5. 用户及用户组及权限
   - useradd 创建用户 用户名 -g 组名–G 次组名-d Home 目录名-p 密码
     ```shell
     useradd gj
     useradd gj –g root –G dba –d /home/gj –p xbrother123
     ```
   - groupadd
     ```shell
     groupadd mongo
     ```
   - passwd
     ```shell
     passwd gj
     ```
   - su 切换用户
     ```shell
     su 用户名
     ```
   - chown 用于更改某个文件或目录的属主和属组
     格式：chown [用户:组] 文件
     ```shell
     chown nobody:nobody ../src
     ```
   - chmod 用于改变文件或目录的访问权限。该命令有两种用法：一种是包含字母和操作符表达式的文字设定法，另一种是包含数字的数字设定法，可用ls -l查看文件的属性
     格式：chmod [who] [+ | - | =] [mode] 文件名
     1 、操作对象who 可以是下述字母中的任一个或者它们的组合：
         u 表示用户(user) ，即文件或目录的所有者
         g 表示同组(group)用户，即与文件属主有相同组ID 的所有用户
         o 表示其他(others)用户
         a 表示所有(all)用户，它是系统默认值。
     2 、操作符号可以是：
         + 添加某个权限
         – 取消某个权限
         = 赋予给定权限,并取消其他所有权限
     3 、 mode 表示权限常用的参数有
         r 可读
         w 可写
         x 可执行
     4 、数字权限格式
         r=4，w=2，x=1 
         rwx = 4 + 2 + 1 = 7
         rw = 4 + 2 = 6
         rx = 4 +1 = 5
     example:
     ```shell
     chmod a+x after.sh
     chmod u=rwx,g=r,o= after.sh
     ```
### 6. 磁盘存储
   - df 命令 查看磁盘空间(diskfree)
     ```shell
     df -lh
     ```
   - du 命令 查看已使用空间(diskused)
     example:
     ```shell
     du -h /opt/log
     du -h /opt/data --max-depth=1
     ```
### 7. 性能监控和优化命令
   - top 命令（htop）查看系统整体运行情况，CPU、内存、进程
   ```shell
   top
   top -p 1234
   ```
   - free 命令
   ```shell
   free -m
   free -h
              total        used        free      shared  buff/cache   available
Mem:           7821         346        3945          16        3529        7076
Swap:          8063           0        8063
   ```
Buffer 是对磁盘数据的缓存，而 Cache 是文件数据的缓存

   - vmstat (VirtualMeomoryStatistics) 内存状态
   ```shell
   vmstat 1
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 1  0      0 4040040   4180 3609660    0    0     0     0    1    2  0  0 100  0  0
 0  0      0 4039892   4180 3609692    0    0     0     0   82  175  0  0 100  0  0
   ```
​	vmstat命令执行结果共分为6部分：procs、memory、swap、io、system、cpu。

​	procs   #进程
​	r(run)：表示运行或等待CPU时间片的进程数，如果该值长期大于服务器CPU的个数，则说明CPU资源不足。一般负载超过了3就比较高，超过了5就高，超过了10就不正常了，服务器的状态很危险；
​	b(block)：表示等待资源的进程数，这个资源指的是I/O、内存等。比如，当磁盘读写非常频繁时，写数据就会变得很	慢，此时CPU运算很快就结束了，但进程需要把计算的结果写入磁盘，这样进程的任务才算完成，此时这个进程只能慢慢地等待磁盘了，这个进程就是这个b状态。该数值如果长时间大于1，则需要去查找问题；

​	memory ：与free命令中的解释类似 

​	swap    #swap空间,单位:KB，内存够用时，si和so值都为0，如果这两个值长期大于0，表示内存不够用了，系统性能会受到影响
​	si：表示从swap空间写入内存的数据量；
​	so：表示从内存写入swap空间的数据库；

​	io      #单位:块/秒
​	bi：每秒读取的块数(读磁盘)，现在的Linux版本块的大小为1024bytes；
​	bo：每秒写入的块数(写磁盘)；

​	system  #系统，这2个值越大，会看到由内核消耗的CPU时间会越大
​	in：每秒CPU的中断次数，包括时间中断；
​	cs：每秒上下文切换数，例如我们调用系统函数，就要进行上下文切换，线程的切换，也要进行上下文切换，这个值越小越好；

​	cpu     #以百分比显示
​	us(user time)：用户进程执行时间；
​	sy(system time)：系统进程执行时间；
​	id：空闲时间(包括IO等待时间)；
​	wa：等待IO时间，wa的值高时，说明IO等待比较严重，这可能由于磁盘大量做随机访问造成的，也有可能是磁盘出现瓶颈；
​	st：表示被偷走的CPU所占百分比(一般都为0，不用关注)；

​	us + sy + id + wa =100%     #这个是只是近似值


   - iostat 
     ```shell
     iostat 1
     iostat -x 1
     avg-cpu:  %user   %nice %system %iowait  %steal   %idle
                0.16    0.00    0.24    0.00    0.00   99.60
     
     Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
     vda               0.04         0.18         0.94     892712    4526875
     dm-0              0.04         0.18         0.93     868612    4479563
     dm-1              0.00         0.00         0.00       2460          0
     dm-2              0.00         0.00         0.01       5038      31893
     dm-3              0.02         0.33         0.21    1593273    1034162
     dm-4              0.00         0.01         0.01      48955      55003
     ```
   - pidstat 输出系统启动后所有活动进程的cpu统计信息
     ```shell
     pidstat 1
     pidstat -r  1
     pidstat -d 1   
     pidstat -r -p 13084 1
     ```
   - lsof (list open files) 列出打开的文件
     ```shell
     lsof | grep xapigo
     ```
   - sar System Activity Reporter（系统活动情况报告）
     ```shell
     sar -u、sar -q cpu信息
     sar -B 、sar-r sar -W 查看内存
     sar -b、sar -u、sar -d 查看IO
     sar -n Dev 1 查看网络实时流量
     ```
   6. 网络命令
   - ifconfig 查看网络基础信息（纯净版centos不带）
     ```shell
     watch ifconfig
     watch cat /proc/net/dev
     ifstat
     ```
   - route 查询、配置路由信息
     ```shell
     route
     route del -net 169.254.0.0 netmask 255.255.0.0 dev eth0
     route add -net 224.0.0.0 netmask 240.0.0.0 dev eth0
     ```
   - traceroute 查询路由
     ```shell
     traceroute www.baidu.com
     ```
   - netstat 查看网络链接状态（纯净版centos不带）
     ```shell
     netstat -lnp
     ```
   - ss 查看网络链接状态
     ```shell
     ss -t -a 显示TCP连接
     ss -u -a 显示所有UDP Sockets
     ss -pl | grep 3306 找出打开套接字/端口应用程序     
     ```
   - ip命令 centos7自带命令
     ```shell
     ip link show  显示网络接口信息
     ip link set eth0 upi  开启网卡
     ip link set eth0 down 关闭网卡
     ip addr show 显示网卡信息
     ip addr add 192.168.0.1/24 dev eth0 
     ip route list 查看路由信息
     ip route add default via 192.168.0.254 dev eth0 
     ip route del 192.168.4.0/24 
     ```
   - scp 远程安全文件拷贝
     ```shell
     scp root@192.168.3.204:/opt/soft/nginx-0.5.38.tar.gz /opt/opt/
     ```
   - wget 文件下载
     ```shell
     wget https://studygolang.com/dl/golang/go1.13.linux-amd64.tar.gz
     ```
   - curl 模拟http协议，也可用于下载
     ```shell
     curl -v http://www.baidu.com >> linux.html
     curl -O https://studygolang.com/dl/golang/go1.13.linux-amd64.tar.gz
     curl -X POST -F upload_file=@xx.file http://192.168.3.27/api/v3/system/version/upload
     curl -H "Content-Type: application/json" -X POST -d '{"username":"xyz","password":"xyz"}' http://localhost/api/login
     ```
   8. 其他命令

   - kill 向进程发信号
     ```shell
     kill 1234
     kill -9 1234
     kill -10 1234
     kill -12 1234
     ```
   - ps 命令查找进程
     ```shell
     ps -aux 显示所有包含其他使用者的行程 
     ps -ef 显示程序间的关系
     ps -o pid,ppid,pgrp,session,tpgid,comm 输出指定字段
     ps -aux | grep xmessage | grep -v grep | awk'{print $2}` | xargs kill -12
     ```
   - wc 统计数量
     ```shell
     ls | wc -l
     ```
   - last 显示登录的人员及时间
   - who 显示当前登录人员及时间
   - ssh 远程登录
   - env 查看环境变量