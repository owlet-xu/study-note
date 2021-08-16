## 系统环境变量影响tomcat默认启动

+ 环境变量路径 /etc/profile
+ 在末尾添加以下内容

```
export CATALINA_HOME=/usr/local/src/tomcat/apache-tomcat-7.0.57     #写Tomcat安装路径
export CLASSPATH=.:$JAVA_HOME/lib:$CATALINA_HOME/lib
export PATH=$PATH:$CATALINA_HOME/bin
```

+ 更新环境变量

  ```
  source /etc/profile
  ```



## 配置Tomcat开机启动

### 方案一

+ ### 将Tomcat配置为系统服务

```
#创建Tomcat8服务文件
vi /usr/lib/systemd/system/tomcat8.service

#tomcat8.service文件内容：

[Unit]
Description=Tomcat8
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=forking

ExecStart=/usr/tomcat/tomcat8/bin/startup.sh
ExecReload=/usr/tomcat/tomcat8/bin/startup.sh
ExecStop=/usr/tomcat/tomcat8/bin/shutdown.sh

[Install]
WantedBy=multi-user.target
```



+ ### 将Tomcat服务配置开机启动

```
#设置Tomcat8开机启动
systemctl enable tomcat8

#启动tomcat8服务
systemctl start tomcat8
```



### 方案二

1、在/etc/init.d下创建服务脚本
`vim /etc/init.d/tomcat`
写入内容如下：

```
#!/bin/bash
#
# tomcat startup script for the Tomcat server
#
#
# chkconfig: 345 80 20
# description: start the tomcat deamon
#
# Source function library
. /etc/rc.d/init.d/functions

prog=tomcat
# 根据自己的路径改写JAVA_HOME
JAVA_HOME=/usr/lib/jvm/jdk1.8.0_161/  
export JAVA_HOME
# 根据自己的路径改写CATALANA_HOME
CATALANA_HOME=/opt/apache-tomcat-8.0.50/   
export CATALINA_HOME

case "$1" in
start)
    echo "Starting Tomcat..."
    $CATALANA_HOME/bin/startup.sh
    ;;

stop)
    echo "Stopping Tomcat..."
    $CATALANA_HOME/bin/shutdown.sh
    ;;

restart)
    echo "Stopping Tomcat..."
    $CATALANA_HOME/bin/shutdown.sh
    sleep 2
    echo
    echo "Starting Tomcat..."
    $CATALANA_HOME/bin/startup.sh
    ;;

*)
    echo "Usage: $prog {start|stop|restart}"
    ;;
esac
exit 0
```

2、更改权限
`chmod a+x /etc/init.d/tomcat`