# 三、Docker 容器管理

1. Docker 基础概念
   Docker 三个重要概念：仓库 (Repository)、镜像 (image) 和 容器 (Container)

   ~~~shell
   docker run --name MyWordPress --link db:mysql -p 8080:80 -d wordpressDocker 
   
   ~~~

   > 指令的基本用法：
   > 	 docker + 命令关键字(COMMAND) + 一系列的参数

2. Docker 基础命令

	> docker info			守护进程的系统资源设置
	> docker search	Docker 	仓库的查询
	> docker pull	Docker 	仓库的下载
	> docker images		Docker 镜像的查询
	> docker rmi			Docker	镜像的删除
	> docker ps			容器的查询
	> docker run			容器的创建启动
	> docker start/stop		容器启动停止
	
	Docker 指令除了单条使用外，还支持赋值、解析变量、嵌套使用

3. 单一容器管理命令
   每个容器被创建后，都会分配一个 CONTAINER ID 作为容器的唯一标示，后续对容器的启动、停止、修改、删除等所有操作，都是通过 CONTAINER ID 来完成，偏向于数据库概念中的主键
   	docker ps --no-trunc					查看
   	docker stop/start CONTAINERID 		停止
   	docker start/stop MywordPress 			通过容器别名启动/停止
   	docker inspect MywordPress   			查看容器所有基本信息
   	docker logs MywordPress  			查看容器日志
   	docker stats MywordPress  			查看容器所占用的系统资源
   	docker exec 容器名 容器内执行的命令  容器执行命令
   	docker exec -it 容器名 /bin/bash  		登入容器的bash

4、Run 常用的一些参数
--restart=always   		容器的自动启动
-h x.xx.xx	 			设置容器主机名
-dns xx.xx.xx.xx	 		设置容器使用的 DNS 服务器
--dns-search				DNS 搜索设置
--add-host hostname:IP	注入 hostname <> IP 解析
--rm						服务停止时自动删除    

5、Docker-Compose
Docker-compose installl
curl -L https://github.com/docker/compose/releases/download/1.14.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
docker version

Docker-compose 用法
-f	    	指定使用的 yaml 文件位置				up -d	    启动容器项目
ps	    	显示所有容器信息						pause	    暂停容器
restart	    重新启动容器							unpause	    恢复暂停
logs	    	查看日志信息							rm	        删除容器
config -q     验证 yaml 配置文件是否正确
stop	    	停止容器
start	    	启动容器


演示代码记录
version: '2'

services:
   db:
     image: mysql:5.7
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
          image: wordpress:latest
          restart: always
          ports:
              - "8000:80"
               environment:
                     WORDPRESS_DB_HOST: db:3306
                     WORDPRESS_DB_USER: wordpress
                     WORDPRESS_DB_PASSWORD: wordpress