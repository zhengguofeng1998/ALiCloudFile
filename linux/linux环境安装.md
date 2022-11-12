# 一、安装jdk

## 1.1、通过yum命令安装

> ```shell
> 1、查看云端yum库中目前支持安装的jdk软件包
> yum search java|grep jdk
> 2、选择安装jdk版本，等待安装完成
> yum install -y java-1.8.0-openjdk*
> 3、查看jdk安装位置
> find / -name 'java'
> 
> 默认路径一般是：
> /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.151-5.b12.el7_4.x86_64/jre/bin/java
> ```
>
> 

## 1.2、通过安装包

> ```
> 下载地址：https://www.oracle.com/cn/java/technologies/javase-downloads.html
> ```
>
> 1、下载安装包
>
> 根据系统版本以及位数选择tar.gz
>
> ![](C:\Users\Administrator\Desktop\study\linux\images\image-0ce0659c9ad74eab81e80d04b1000db2.png)
>
> 复制下载链接
>
> ![](C:\Users\Administrator\Desktop\study\linux\images\image-971d274b30404abcb2618a5eff5e4fc3.png)
>
> ```shell
> mkdir /usr/java
> cd /usr/java
> wget https://download.oracle.com/otn/java/jdk/8u271-b09/61ae65e0886
> ```
>
> 2、解压
>
> ```shell
> tar zxvf jdk-8.0.1_linux-x64_bin.tar.gz
> ```
>
> 3、配置环境变量
>
> ```shell
> vim /etc/profile
> 在文章末尾处添加（注意地址是自己的jdk安装路径的对应地址）
> export JAVA_HOME=/usr/share/jdk1.6.0_14
> export PATH=$JAVA_HOME/bin:$PATH
> export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
> ```
>
> 4、使profile文件生效,或重启
>
> ```shell
> source /etc/profile
> ```
>
> 5、验证是否安装成功
>
> ```shell
> java -version
> ```

# 二、安装GIT

# 三、安装Mysql

# 四、安装nginx

# 五、安装maven

# 六、安装redis

## 6.1、安装redis

1、去redis官网：https://redis.io/download/

2、下载资源,并解压

```shell
wget https://github.com/redis/redis/archive/7.0.5.tar.gz
解压
tar -zvxf redis-5.0.7.tar.gz
```

3、 安装 

```shell
cd 安装目录如我的 /usr/local/redis/redis-7.0.5
make
cd src
make install PREFIX=/usr/local/redis/redis-7.0.5
```

这时就可以通过命令启动了

```shell
1、启动
./redis-server
2、客户端链接
2、redis-cli -h 127.0.0.1 -p 6379 -a 密码（可以在配置文件设置，默认没有密码）
```

## 6.2、远程客户端链接redis

1、修改`redis.conf`配置文件

第一处，需要开启地址授权，可以将`bind 127.0.0.1`注释掉或者是将后面的ip改成`0.0.0.0`。这样表示所有的ip都能访问该redis服务，否则只有本机可以访问。

第二处，将`protected-mode`的值改成`no`，默认为`yes`

第三处（可有可无），设置密码   `requirepass`  后面的就是密码，可以更改成自己的

2、防火墙设置

```shell
1、查看防火墙状态
systemctl status firewalld
2、查看防火墙是否开放了6379端口号
firewall-cmd --query-port=6379/tcp
3、若没开放则开放端口号
firewall-cmd --zone=public --add-port=6379/tcp --permanent
4、重启
firewall-cmd --reload
5、关闭、开启防火墙（重启就行了这儿不用）
systemctl start firewalld
systemctl stop firewalld
```

3、阿里云安全组设置

![](C:\Users\Administrator\Desktop\study\linux\images\微信截图_20221111152323.png)

# 七、安装nacos

# 八、安装mongoDB

# 九、安装RabbitMQ