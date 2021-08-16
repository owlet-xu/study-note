## 查看centos版本

```
cat /etc/os-release
cat /etc/redhat-release
cat /proc/version
## 查看内存
cat /proc/meminfo |grep MemTotal
## 查看cpu
cat /proc/cpuinfo |grep "model name" && cat /proc/cpuinfo |grep "physical id"
```

## 查看进程，杀死进程，查看进程网络端口状态

```
ps -aux|grep java
kill xxxx
## 查看端口被哪个进程占用
netstat -lnp|grep 8000
## 查看进程占用哪个端口
netstat -nap | grep 进程pid
```





## 开放端口给其他用户链接

```
firewall-cmd --zone=public --add-port=6379/tcp --permanent

firewall-cmd --reload

```

## 可重启服务器验证自动启动

```
# 立刻重启(root用户使用)
shutdown -r now
# 重启
reboot
```

## 搜索文件

find 指定目录 指定条件 指定动作

Find ./ -name ‘interfaces’

例如：

```
find ./ -name gaobaiqiqiu.mp3
```

## ls或ll查看文件详情

查看当前文件夹ssm.log 的大小

```
ls -lh ssm.log 
```



# **修改root密码**

```
// 1、切换root用户，并输入密码
su root
18255153428xgy
// 2、登录成功$变成#号
// 3、修改密码
 sudo passwd root
```



# **查看文本文档**

1、Cd 到相关目录，命令  vi aaa.txt 

2、显示内容时候  按 【i】  键（insert）编辑文本

3、按 【Esc】退出编辑，输入【：q】退出，输入【：wq】写入退出  输入　:wq ! 强制写入  输入 :q！强制退出不保存

4、【:set fileencoding】  查看文本编码

5、vim中的编辑模式中 按住 shift + insert 插入剪贴板的内容



# **cp mv rm mkdir命令**

 -r:递归操作

 -f:强制的意思（force）,也就是说覆盖掉已存在的文件

-i:删除时给出提示信息

 -n:若目标文件存在，不覆盖

  -u:若源文件比目标文件新，或者目标文件丢失，则更新，否则不更新

+ 复制

  ```
  # 将/opt/a/下的a.录复制到 /opt/b/目录
  cp -r /opt/a/ /opt/b/ **
  ```



+ 移动

  ```
  # 在同一个目录下，mv还有改名的功能
  mv [-finu] source destination
  ```

  

+ 删除

  ```
  # 这个命令是非常危险的，除非非常确定， 否则建议加上i选项
  rm -rf file/dir
  ```

+ 创建目录

  ```
  ## 当前目录下创建work文件夹
  mkdir work   
  ```

  

# **Tomcat安装  解压**

1、官网下载安装压缩包  apache-tomcat-9.0.2.tar.gz



# **Linux查看ip和ping**

Ifconfig 

ping 192.168.1.100 会一直ping   

ctr + c  取消

## vi操作

+ 1、Cd 到相关目录 vi aaa.txt 

+ 2、显示内容时候,按【i】键（insert）编辑文本

+ 3、按【Esc】退出编辑，

  输入【:q】退出，

  输入【:wq】写入退出  

  输入【:wq!】强制写入  输入【:q！】强制退出不保存

+ 4、【:set fileencoding】  查看文本编码



## 防火墙

```
# 开放6379端口
firewall-cmd --zone=public --add-port=6379/tcp --permanent
# 重启防火墙
firewall-cmd --reload
# 查看防火状态
systemctl status firewalld
# 永久关闭防火墙
systemctl stop firewalld
systemctl disable firewalld
chkconfig iptables off
# 重启防火墙
systemctl enable firewalld
service iptables restart 
```

## 查看端口通不通

```
curl 172.21.9.153:8080
# empty reply from server 是通的，其他返回不通
```

## 打印日志

```
tail -f nohup.out
```



## 权限问题

```
# 从别的contos拷贝包运行会有Permission denied错误
# 需要给这个文件附上权限
chmod +x ./console
```



## nginx 操作

```
#重启
./nginx -s reload
#快速停止nginx
nginx -s stop
#完整有序的停止nginx
nginx -s quit 
# 启动nginx
./nginx
```

## 安装node

1、下载安装包node-v10.15.3-linux-x64.tar.xz

2、在  /usr/local/node  文件夹解压

```
xz -d node-v10.15.3-linux-x64.tar.xz
tar -xvf node-v10.15.3-linux-x64.tar
```

3、把bin目录添加到PATH环境变量

```
vi /etc/profile
#在最后添加  export PATH=/usr/local/lib/nodejs/bin:$PATH
#保存执行
source /etc/profile
```

4、验证

```
node -v
npm version
npx -v
```

## 错误修改 profile commd not found

```
#第一步： 
export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin 
#第二步：
/bin/vi /etc/profile
#第三步：保存执行 
source /etc/profile
```

