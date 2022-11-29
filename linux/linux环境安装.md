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
> ![](images\image-0ce0659c9ad74eab81e80d04b1000db2.png)
>
> 复制下载链接
>
> ![](images\image-971d274b30404abcb2618a5eff5e4fc3.png)
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

暂不需要

# 三、安装Mysql

太难了，自行百度吧

# 四、安装nginx

## 4.1、方法一：使用yum安装

1、安装nginx

```shell
$  yum -y install nginx   # 安装 nginx
$  yum remove nginx  # 卸载 nginx
```

```shell
systemctl enable nginx # 设置开机启动 
systemctl start nginx    # 启动
systemctl stop nginx	# 停止
systemctl restart nginx	#重启
systemctl status nginx	#查看状态
```

安装成功后，默认的网站目录为： /usr/share/nginx/html

默认的配置文件为：/etc/nginx/nginx.conf

自定义配置文件目录为: /etc/nginx/conf.d/

## 4.2、方法二：安装包安装

1、安装nginx所需要的环境

```shell
yum -y install pcre pcre-devel # 让 nginx 支持重写功能
# zlib 库提供了很多压缩和解压缩的方式，nginx 使用 zlib 对 http 包内容进行 gzip 压缩
yum -y install zlib zlib-devel 
# 安全套接字层密码库，用于通信加密
yum -y install openssl openssl-devel
```

2、下载nginx压缩包

```shell
https://nginx.org/en/download.html
tar -zxvf nginx-1.11.5.tar.gz #解压缩
```

3、验证环境

```shell
cd nginx-1.11.5
./configure --prefix=/usr/local/nginx # 检查平台安装环境
注：
	--prefix=/usr/local/nginx 是编译后安装的目录
```

4、编译安装nginx

```shell
make # 编译
make install # 安装
```

5、nginx启动等命令

```shell
nginx # 启动
nginx -c /usr/local/nginx/conf/nginx.conf # 指定配置文件启动
nginx -s stop # 停止
nginx -s restart # 重启
nginx -s reload #重启并加载配置文件
```

# 五、安装maven

暂不需要

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

![](images\微信截图_20221111152323.png)

# 七、安装nacos

1、下载安装包

```shell
https://github.com/alibaba/nacos/releases  # 网址
tar -zxvf nacos-server-2.1.2.tar.gz 解压安装包
```

2、启动nasoc

```shell
在bin目录下,单机启动
./startup.sh -m stanalone 
```

3、开放端口

开启防火墙以及阿里云控制台的防火墙策略

# 八、安装mongoDB

# 九、安装RabbitMQ

# 十、安装seata

# 十一、安装 Elasticsearch

# 十二、安装Jenkins

# 十三、安装xxl-job定时任务

# 十四、安装docker

1、下载需要的安装包

```shell
yum install -y yum-utils
```

2、设置阿里云镜像仓库

```shell
yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

3、更新yum软件包索引

```shell
yum makecache fast
```

4、安装社区版docker相关的配置

```shell
 yum install docker-ce docker-ce-cli containerd.io
```

5、启动docker

```shell
# 启动docker
systemctl start docker
# 查看当前版本号，是否启动成功
docker version
# 设置开机自启动
systemctl enable docker
```

6、配置阿里云镜像加速(一次执行一下四条命令)

```shell
sudo mkdir -p /etc/docker

sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://axvfsf7e.mirror.aliyuncs.com"]
}
EOF

sudo systemctl daemon-reload

sudo systemctl restart docker
```

7、相关命令

```shell
# 查看所有镜像
docker images
# 下载镜像
docker pull tomcat
# 指定版本下载
docker pull mysql:5.7
# 删除镜像
	#1.删除指定的镜像id
	docker rmi -f  镜像id
	#2.删除多个镜像id
	docker rmi -f  镜像id 镜像id 镜像id
	#3.删除全部的镜像id
	docker rmi -f  $(docker images -aq)
# 运行容器
docker run [可选参数] image
    #参数说明
    --name="名字"           指定容器名字
    -d                     后台方式运行
    -it                    使用交互方式运行,进入容器查看内容
    -p                     指定容器的端口
    (
    -p ip:主机端口:容器端口  配置主机端口映射到容器端口
    -p 主机端口:容器端口
    -p 容器端口
    )
    -P                     随机指定端口(大写的P)
# 进入到运行中的容器中
docker exec -it tomcat /bin/bash
# 推出容器
exit
# 列出正在运行中的容器
docker ps
# 列出所有运行过的容器
docker ps -a
#删除指定的容器
docker rm 容器id
#删除所有的容器
docker rm -f $(docker ps -aq)
#删除所有的容器
docker ps -a -q|xargs docker rm
#启动容器
docker start 容器id
#重启容器
docker restart 容器id
#停止当前运行的容器
docker stop 容器id
#强制停止当前容器
docker kill 容器id
```

# 通用设置

## 防火墙操作

```shell
firewall-cmd --state # 查看防火墙状态
firewall-cmd --reload # 重启防火墙
systemctl enable firewalld.service # 设置开机自启
firewall-cmd --zone=public --add-port=80/tcp --permanent # 开放80端口
```



