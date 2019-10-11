# 二、Docker 安装

1. Docker 的安装方式

   * Script Install

     > yum update

     > $ curl -sSL https://get.docker.com/ | sh
     > systemctl start docker
     > systemctl enable docker
     > docker run hello-world

   * YUM Install

     > yum update

     > ~~~shell
     > cat >/etc/yum.repos.d/docker.repo <<-EOF
     > [dockerrepo]
     > name=Docker Repository
     > baseurl=https://yum.dockerproject.org/repo/main/centos/7 
     > 
     > enabled=1 
     > gpgcheck=1 
     > gpgkey=https://yum.dockerproject.org/gpg EOF
     > ~~~

     > yum install docker

   * RPM Install
     <https://download.docker.com/linux/centos/7/x86_64/stable/Packages/>

   

2. Docker 镜像加速配置

   > ~~~shell
   > cp /lib/systemd/system/docker.service  /etc/systemd/system/docker.service
   > ~~~
   >
   > ~~~
   > chmod 777 /etc/systemd/system/docker.service 
   > ~~~
   >
   > ```shell
   > vim    /etc/systemd/system/docker.service   
   > ```
   >
   >  ExecStart=/usr/bin/dockerd-current  --registry-mirror=https://kfp63jaj.mirror.aliyuncs.com \
   >
   > ~~~shell
   > systemctl   daemon-reload
   > ~~~
   >
   > ~~~ shell
   > systemctl   restart   docker
   > ~~~
   >
   > ```shell
   > ps   -ef   |   grep docker
   > ```
   >
   > 阿里云Docker官网：https://dev.aliyun.com/search.html



3. Docker 化应用体验
  环境分析
  WordPress 运行环境需要如下软件的支持：

  * PHP 5.6 或更新软件

  + MySQL 5.6 或 更新版本

  + Apache 和 mod_rewrite 模块

  代码展现

  ~~~shell
  docker run --name db --env MYSQL_ROOT_PASSWORD=example -d mariadb
  docker run --name MyWordPress --link db:mysql -p 8080:80 -d wordpress
  ~~~

