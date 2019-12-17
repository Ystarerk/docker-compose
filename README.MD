# windows 7 VirtualBox安装CentOS搭建基于docker的nginx, php运行环境

```
包含的软件：
nginx
php（可选php 5.*或php 7.*）
phpredis扩展（php5.*安装小于2.2.8的版本 php7.*安装>=3.0的版本）

```

# 基础软件环境

```
Windows 7
VirtualBox

注意：因为Win10有Docker特别版，此环境只适用于Win7

```

# 安装步骤简要说明

```
安装好VitrualBox后
配置虚拟机 安装CentOS 7
设置虚拟机的共享文件夹，固定分配
c/Users => E:\work  /* E:\work是自己的win7代码目录，改为自己机器上的目录 */
自动挂载 = 是
访问权限 = 完全
重启虚拟机

进入CentOS 7后，共享文件夹自动挂载到了 /media/sf_work/

CentOS 7有SELinux安全机制，需要调整到宽容模式
$ echo "/usr/sbin/setenforce 0" >> /etc/rc.local

设置开机可运行 rc.local
$ chmod +x /etc/rc.d/rc.local
```

# HOSTS指向

修改 C:\Windows\System32\drivers\etc\hosts
192.168.99.100 是虚拟机IP
```
192.168.99.100 www.beta.com www.dev.com
192.168.99.100 login.beta.com login.dev.com
192.168.99.100 api.beta.com api.dev.com
192.168.99.100 buy.beta.com buy.dev.com
192.168.99.100 static.beta.com static.dev.com
192.168.99.100 ex.beta.com ex.dev.com
192.168.99.100 exapi.beta.com exapi.dev.com
192.168.99.100 front.beta.com front.dev.com
192.168.99.100 m.beta.com m.dev.com
```

# 启用环境

```shell
#用git工具下载此项目
#例如：
#在 /media/sf_work/ 执行git命令
$cd /media/sf_work
$git clone http://labs.oa.com/tobin/docker-compose.git

#下载完成后生成目录
#/media/sf_work/docker-compose

#进入docker-compose目录
$cd docker-compose

#第一次运行
#编译
$docker-compose build
#等待编译完成，启动后台运行（-d 是后台运行）
$docker-compose up -d
#第一次运行完成
#下一次开机启动docker的命令
$docker-compose start
```

# 目录文件作用说明

```
mysql  --------------- mysql
    Dockerfile              mysql docker 配置文件（未启用）
nginx  --------------- nginx
    logs ------------- nginx log目录
    vhost ------------ nginx 多域名配置文件
        api.conf              api.dev.com api.beta.com配置文件
        buy.conf              buy.dev.com buy.beta.com配置文件
        ex.conf              ex.dev.com ex.beta.com配置文件
        exapi.conf              exapi.dev.com exapi.beta.com配置文件
        front.conf              front.dev.com front.beta.com配置文件
        static.conf              static.dev.com static.beta.com配置文件
        www.conf              www.dev.com www.beta.com配置文件
    Dockerfile              nginx docker 配置文件
    nginx.conf              nginx 配置文件
    php.conf              nginx php-fpm 配置文件
php  ----------------
    Dockerfile              php 5.*-fpm docker 配置文件
php7  ----------------
    Dockerfile              php 7.*-fpm docker 配置文件
redis  -------------- redis server
    Dockerfile              redis docker 配置文件（未启用）
```