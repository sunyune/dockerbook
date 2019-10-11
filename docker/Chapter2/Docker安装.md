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

     > cat >/etc/yum.repos.d/docker.repo <<-EOF
     > [dockerrepo]
     > name=Docker Repository
     > baseurl=https://yum.dockerproject.org/repo/main/centos/7 
     >
     > enabled=1 
     > gpgcheck=1 
     > gpgkey=https://yum.dockerproject.org/gpg EOF

     > yum install docker

   * RPM Install
     <https://download.docker.com/linux/centos/7/x86_64/stable/Packages/>

   

2. Docker 镜像加速配置

   > cp /lib/systemd/system/docker.service  /etc/systemd/system/docker.service
   >
   > chmod 777 /etc/systemd/system/docker.service 
   >
   > vim    /etc/systemd/system/docker.service   	
   >     ExecStart=/usr/bin/dockerd-current  --registry-mirror=https://kfp63jaj.mirror.aliyuncs.com \ 
   >
   > systemctl   daemon-reload
   >
   > systemctl   restart   docker
   >
   > ps   -ef   |   grep docker
   >
   > 阿里云Docker官网：https://dev.aliyun.com/search.html