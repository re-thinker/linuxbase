1. ### 目录管理命令:mkdir、rmdir
	
   - mkdir 创建新的目录	
	  Usage: mkdir [OPTION]... DIRECTORY
	  example:
	  
	  ```shell
	  mkdir /tmp/test1
	  mkdir -pv  /opt/log/test1/test2/test3 
	  ```
	  
	- rmdir 删除空目录
	  Usage: rmdir [OPTION]... DIRECTORY.
	  example:
	  
	  ```shell
	  rmdir  /tmp/test1
	  rmdir -p /opt/log/test2/test3
	  ```
	  注：只能删除空目录，目录中有文件时，无法删除
	
2. ### 文件管理命令:cp、mv、rm
	- cp 复制命令
	  example:
      ```shell
      cp /opt/log/xmessage.log /opt/
      cp -r /opt/log/test1 /opt/
      ```
     
    - mv 移动目录或文件，引申的功能是给目录或文件重命名
      example:
      ```shell
      mv /opt/log/xmessage.log /opt/log/xmessage.log.bak
      ```
    - rm 用来删除文件的，rm命令常用的参数有三个-i,-r,-f
   	  example:
      ```shell
      rm /opt/log/xmesssage.log.bak
      系统会询问我们是否要删除xmesssage.log.bak 文件，敲了“y/n” 确认是否要删除xmesssage.log.bak 
      rm -r /opt/log/test1
      rm -f /op/log/test1
      ```
      注：使用rm -rf 时一定要注意确认，删除的文件无法恢复，根目录是可以直接删除的
3. ### 目录查看 ls、cd、pwd
     - ls 查看目录下的文件  最常用的参数有三个:-a、 -l 、–F 和 h
       example:
       ```shell
       ls -hl /opt/log
       ls -al /root
       ```
     - cd 进出目录
       example:
       ```shell
       cd ~/
       cd -
       pwd
       ```
4. ### 文件查看命令 cat、more、less、tail、head
     - cat 它的功能是显示或连结一般的ascii 文本文件
       example:
       ```shell
       cat /etc/profile
       ```
       example 分隔合并文件，配合split命令：
       ```shell
       split -b 30M typora-setup-x64.exe
       cat file1 file2 > typora-setup-x64.exe
       ```
     - more、less 如果一个文本文件太长了超过一个屏幕的画面，可以more、less分屏查看，less功能更强大，支持搜索
     - tail、head，从尾、从头查看文件内容，常用-n选项，显示多少，tail 还有个-f命令，用于跟踪文件变化，常用于查看程序实时日志
       example
       ```shell
       tail -f xmessage.log
       tailf xmeessage.log
       ```
       注：tail -f 经常被使用，有个独立的tailf程序
5. ### 用户及用户组 useradd、userdel、groupadd、groupdel、passwd
     - useradd 创建用户 用户名 -g 组名–G 次组名-d Home 目录名-p 密码
       example:
       ```shell
       useradd gj
       useradd gj –g root –G dba –d /home/gj –p xbrother123
       ```
     - groupadd
       example:
       ```shell
       groupadd mongo
       ```
     - passwd
       example:
       ```shell
       passwd gj
       ```
6. ### 更改权限 useradd、userdel、groupadd、groupdel、passwd